# ADR-0018: The adapter states a CORS policy — wildcard origins, no credentials

- **Status:** accepted
- **Date:** 2026-08-21
- **Deciders:** engine maintainer
- **Related:** PRJ-175, ADR-0011 (Phase 8 scope, the adapter's non-goals),
  ADR-0016 point 4 (every endpoint is ungated, and that is a decision, not an
  omission), `client/to-engine/008`, `client/to-client/010`

## Context

`client/to-engine/008` reports that `runtime/api.py` sends no
`Access-Control-*` headers at all, so no browser can call it: a preflight
`OPTIONS /games` comes back `405`, and a real `POST /games` succeeds with no
CORS headers on the response, which a browser then discards. This is not a
misconfiguration — there is no header to configure — and neither test suite
catches it, because both drive the adapter through clients that are
structurally incapable of enforcing same-origin policy: FastAPI's
`TestClient` calls the ASGI app in-process, and the client's own live-engine
script runs under node, which does not enforce it either. The one client the
adapter exists for — a browser — is the one client neither suite uses.

The client is unblocked in the meantime with a Vite dev-server proxy,
explicitly labelled a stopgap: it fixes same-origin for local development and
does nothing for a client served from a real origin later. The report asks
the engine to decide three things rather than have the client guess: which
origins to allow, note that the WebSocket path is unaffected either way, and
whether a contract-proving adapter should even carry this concern versus
pushing it to a deployment-time proxy.

That third question is the one worth answering first, because it decides
whether the other two are this ADR's business at all. ADR-0011 draws the
adapter's non-goal line at "rich API concerns — auth, lobbies, matchmaking,
persistence, multiplayer session management." CORS is not on that list, and
for a good reason: those are all concerns of a *product* server standing
between users. CORS here is not that — it is the browser's enforcement
mechanism for the *same* seam ADR-0011 §7 built the adapter to cross. The
module docstring already says the adapter exists because "the separate
web-UI repo cannot [bind in-process]." A response the target browser is
structurally unable to read is that seam not actually crossed, just declared
crossed. Silence is not neutrality here — it is an unstated position, and
that is the state the report is naming as the only unworkable one.

## Decision

`runtime/api.py` adds `fastapi.middleware.cors.CORSMiddleware` to
`create_app()`, with a wildcard origin and no credentials:

```python
from fastapi.middleware.cors import CORSMiddleware

app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],
    allow_methods=["GET", "POST", "OPTIONS"],
    allow_headers=["content-type"],
)
```

- **Origins: wildcard, not a dev-origin allowlist.** Consistent with ADR-0016
  point 4 — every endpoint is already unauthenticated and open to anyone who
  knows a game id; a CORS allowlist would gate *origin* on a resource that
  gates nothing else, which is a policy the adapter does not otherwise have
  and cannot enforce (a non-browser client ignores CORS entirely, so the
  allowlist would only ever inconvenience a browser, never an attacker).
- **No credentials.** `allow_credentials` is left at its default `False`. The
  adapter has no cookies, sessions, or bearer auth to carry, and the CORS
  spec forbids combining a wildcard origin with `allow_credentials=True`
  anyway — so this is not a narrowing, it is naming the state that was
  already true.
- **The WebSocket path is unchanged.** `CORSMiddleware` governs HTTP only;
  the `/ws` route keeps whatever behavior Starlette gives it today (it
  connects regardless of `Origin`, per the report). That asymmetry — HTTP
  gated by a header, WS gated by nothing — is now a known, documented
  property of the adapter rather than a surprise the next client finds on
  their own, but closing it is not this ADR's job: it would mean adding the
  adapter's first origin check anywhere, which is a stricter posture than
  the wildcard HTTP policy this ADR just chose, not a looser one, and deserves
  its own decision if it is ever wanted.
- **This lives in the adapter, not a deployment proxy.** The adapter is
  responsible for being reachable by the client ADR-0011 §7 built it for; a
  reverse proxy is a legitimate way to run it in production, but it is not a
  substitute for the adapter stating a policy of its own. the client's Vite
  proxy remains exactly what it called itself — a dev-only stopgap for
  same-origin, not a CORS policy.

## Rationale

**Wildcard over an allowlist, because the allowlist would be theater.** An
allowlist reads as tighter, but it only restricts the one class of client
that respects CORS — browsers running well-behaved JavaScript — while doing
nothing against a script that just doesn't send an `Origin` header, or sends
whatever `Origin` it likes. The adapter's actual security posture is "open to
anyone who knows a game id," decided already in ADR-0016; an origin allowlist
would dress that up without changing it, and would need revisiting every time
the client's dev port or hosting origin changes — cost with no matching
benefit. If the adapter ever gets real auth, CORS gets reconsidered alongside
it, because at that point credentials come into play and the wildcard
combination stops being legal regardless.

**In the adapter, not behind a proxy, because the seam is the adapter's job.**
The proxy-instead argument is reasonable in general — plenty of production
CORS policy lives at a reverse proxy or CDN edge — but ADR-0011 already
decided this adapter's purpose is to be the thing a separate client repo
binds to. A version of the adapter that only works with an operator-supplied
proxy in front of it is not fully proving the contract it claims to prove;
it is proving the contract-plus-proxy. Stating the header here keeps "can a
browser reach this adapter" answerable by running the adapter alone, which is
the same reason the adapter has a `TestClient` suite instead of requiring a
deployed environment to test against.

## Consequences

- **Positive:** a browser client can call every HTTP endpoint cross-origin
  without any client-side workaround. the client's dev proxy becomes optional
  rather than load-bearing, though the client may keep it for other reasons.
- **Positive:** the policy is uniform and requires no maintenance as client
  dev ports or future hosting origins change.
- **Positive:** matches the adapter's existing, already-decided security
  posture (ADR-0016 point 4) instead of inventing a second, inconsistent one.
- **Negative:** any browser page, on any origin, can drive any game whose id
  it knows — but this is not a new exposure. It was already true for
  non-browser clients and for a browser page served same-origin with the
  engine; this ADR just stops browsers being the one client class
  accidentally excluded.
- **Negative:** the HTTP/WebSocket asymmetry (one now states a policy, the
  other states none) persists and is now documented rather than closed.
- **Neutral:** `fastapi.middleware.cors.CORSMiddleware` is a `fastapi`-bundled
  dependency already installed for Phase 8 (ADR-0011 §7) — no new package.

## Alternatives considered

### Alternative 1: an explicit dev-origin allowlist

`allow_origins=["http://localhost:5173", "http://127.0.0.1:5173"]`, as the
report's own suggested snippet used. Rejected as the *default*: it is tighter
in appearance only (see Rationale), and it silently breaks the day the client
is served from any other origin — a production build, a different dev port,
a preview deploy — turning a header decision into a recurring maintenance
item for a repo whose adapter has no other origin-based policy to keep it
consistent with. Revisit if/when the adapter gains credentialed auth, since
wildcard + credentials is not legal CORS regardless of preference.

### Alternative 2: no CORS headers — a proxy is the permanent arrangement

Say plainly that this is a deployment concern and instruct every client to
run a same-origin proxy in front of the adapter, matching the report's
offered fallback. Rejected per the Rationale above: it would mean the
contract-proving adapter, run alone, cannot be reached by the client it
exists for, which is a bigger non-goal than ADR-0011 actually drew.

### Alternative 3: gate the WebSocket origin to match HTTP

Add an explicit `Origin` check in the `/ws` handler so both transports carry
the same policy. Rejected for this ADR: the wildcard HTTP policy just chosen
permits every origin anyway, so a matching WS check would be a no-op today
and pure added code. Worth doing only if the HTTP policy ever narrows past
wildcard, at which point the two should be reconsidered together.

## Migration

PRJ-175 carries it: `CORSMiddleware` added in `runtime/api.py::create_app`,
plus a preflight-`OPTIONS` integration test asserting
`Access-Control-Allow-Origin` is present — the test-suite gap the report
identified, closed the same way ADR-0016's `spectator` viewer closed the
union-of-views gap: by making the adapter's own suite exercise the surface
the previous suite structurally could not.

No existing caller changes behavior: `CORSMiddleware` only adds response
headers and answers preflight `OPTIONS` requests; every existing `TestClient`
assertion on status codes and bodies is unaffected.
