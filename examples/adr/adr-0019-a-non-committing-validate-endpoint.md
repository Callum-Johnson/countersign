# ADR-0019: A non-committing `/validate` endpoint mirrors `/actions`

- **Status:** accepted
- **Date:** 2026-08-21
- **Deciders:** engine maintainer
- **Related:** PRJ-177, PRJ-159 (the adapter), PRJ-154 (action wire),
  `client/to-client/015`, `client/to-engine/011`

## Context

The UI/UX design spec forwarded to the client (`client/UI_UX_DESIGN_SPEC.md`)
requires a movement/action preview loop: the player sees ghost positions, an
intent arrow, and a legality readout *before* committing, with an explicit
Cancel/Confirm step. `client/to-engine/011` confirms this is a hard blocker
for their Milestone 3 movement slice and rules out the alternative of faking
it client-side — holding a candidate action locally and treating "no
rejection yet" as legality, since that has no rollback if the client guesses
wrong and would require reimplementing coherency/engagement-range/terrain
legality in TypeScript, which is exactly the rule-duplication this project's
own conventions forbid.

The engine already has what a preview needs: `apply_action(state, action) ->
ActionResult` is a pure function. Nothing commits until a caller adopts
`result.new_state`. The gap is only that `runtime/api.py`'s `POST
/games/{id}/actions` goes through `GameRunner.submit()`, which *does* mutate
the held session state on `status == "applied"`. There is currently no HTTP
path to get `apply_action`'s answer without it becoming real.

## Decision

**Add `POST /games/{id}/actions/validate`, taking the identical PRJ-154
action payload `/actions` takes, that calls `apply_action` directly against
the session's current state and returns the same status/errors shape —
without ever touching `GameRunner`'s held state or broadcasting to
listeners.**

```
POST /games/{id}/actions/validate    {<same body as /actions>}
  -> 200 {"status": "applied" | "invalid" | "awaiting_input",
          "errors": [{"rule_id": ..., "description": ...}]}   # invalid only
```

To confirm for real, the client POSTs the identical payload to the existing
`/actions`. Two calls, one payload, one meaning: the first asks "what would
happen", the second makes it happen.

Three things about the shape are load-bearing:

1. **It reads `session.runner.state` and calls `apply_action` directly** — it
   does not go through `GameRunner.submit()` at all, so there is no path by
   which `status: applied` from this endpoint could be mistaken for a
   committed state or leave the session's `_awaiting`/`_log` touched.
2. **No broadcast.** `/actions` pushes a fresh view to every WebSocket
   listener after a real change (PRJ-159's broadcast-on-change). This
   endpoint never calls `_broadcast` — nothing changed, so nobody is told
   anything changed.
3. **The response omits `view`.** `/actions` returns `{"status", "view"}`;
   this endpoint returns `{"status", "errors"}` and no `view`, because there
   is no new state to view — echoing back the unchanged current view would
   invite a client to treat it as fresh.

## Rationale

**A twin endpoint over a `dry_run` flag on `/actions`.** A boolean that
changes whether a request is real is an easy thing to get backwards once
(send `dry_run: true` in a confirm click, or omit it on a preview click) with
a silent, expensive failure mode — an accidental real commit. A distinct path
makes the two calls visually and structurally different at every call site,
and keeps `/actions`'s existing contract (every successful call is real)
completely unchanged for any caller that has never heard of validation.

**Calling `apply_action` directly rather than adding a "peek" mode to
`GameRunner`.** `GameRunner.submit` exists specifically to fold a *committed*
transition into held state (§DESIGN 3.6-adjacent: the runner is a session, not
a pure function). Teaching it to sometimes not commit would mean auditing
every place `submit`'s side effects are assumed — this endpoint sidesteps that
entirely by not calling it.

**This closes the one alternative `to-engine/011` explicitly rejected** —
client-side legality guessing — for the reason they gave: it cannot be undone
if wrong, and reimplementing rule logic client-side is the exact duplication
this project's engine-is-authoritative principle (DESIGN §1, priority 1) exists
to prevent.

## Consequences

- **Positive:** unblocks the movement half of the client's Milestone 3 first
  slice (`TAC-025` et al., per `to-engine/011`).
- **Positive:** no `ACTION_VERSION`/`VIEW_VERSION` bump — the endpoint is new,
  the existing action wire is reused unchanged, and `/actions` itself is
  untouched.
- **Positive:** the response shape is a strict subset of `/actions`'s
  existing `invalid` error body, so nothing new needs inventing on the errors
  side.
- **Neutral:** a second HTTP round trip per preview cycle (validate, then
  confirm submits again). Accepted — the alternative (guessing client-side)
  was rejected on the merits, not on latency grounds, and this is a local/dev
  adapter, not a product server under load.
- **Negative:** a caller could poll `/validate` in a tight loop as a
  read-only oracle for legality without ever meaning to act — harmless
  (no state changes, nothing broadcasts) but worth naming since the adapter
  is otherwise ungated (ADR-0016 point 4) and this is one more unauthenticated
  read-shaped call.

## Alternatives considered

### Alternative 1: `dry_run: true` flag on the existing `/actions`

Rejected — see Rationale. A same-shaped request whose realness hinges on one
boolean is the shape of bug that only shows up once, expensively.

### Alternative 2: client holds candidate actions and treats "no error yet" as legal

The alternative `client/to-engine/011` itself rejected. No rollback on a
wrong guess, and it requires re-deriving coherency/engagement-range/terrain
legality client-side — a second, drifting copy of rules this engine already
owns.

### Alternative 3: `GameRunner` grows a `peek(action) -> ActionResult` method

Considered and folded into the Decision instead of kept as a rejected
alternative — this is really the same idea as calling `apply_action` directly,
just routed through the runner. Not adding it to `GameRunner`'s public surface
because nothing else needs a peek capability yet; the adapter can call
`apply_action` itself without the runner mediating.

## Migration

PRJ-177 carries it: one new route in `runtime/api.py`, no existing route's
behaviour changes, no wire version moves. Announced in `client/to-client/016`
alongside ADR-0020.
