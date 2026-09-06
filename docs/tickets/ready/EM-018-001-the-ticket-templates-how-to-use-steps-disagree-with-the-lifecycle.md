---
id: EM-018-001
title: The ticket template's how-to-use steps disagree with the lifecycle on three points
status: ready
tier: standard
complexity: S
dependencies: []
---

# EM-018-001 — The ticket template's how-to-use steps disagree with the lifecycle on three points

## Context

Raised while working EM-018, from reading `templates/TICKET.md` whole after
its references were repointed at 2480575. EM-018 made the template's
references resolve; it left what the template's "How to use this template"
steps say to do, which was out of its scope. Three of those instructions
contradict `docs/ticket-lifecycle.md`, the document the template now sends
its reader to for the procedure:

- Step 5 says to commit on a `docs/ticket-PRJ-XXX` branch, or directly to
  `master`. The lifecycle's "Claiming" step 1 and the contributor policy's
  §7 checklist require a branch whose name begins with the ticket
  identifier, and this repository's default branch is `main`.
- Step 1 finds the next lineage id with `ls docs/tickets/*/PRJ-284-*` and the
  next flat id as the highest across the four directories. The lifecycle's
  "Lineage" section says the next id comes from history, not the tree, with
  `git log --diff-filter=A --name-only --format= -- docs/tickets`, and
  records the reused id that taught it.
- The PR Description note says a `PR.md` draft at the worktree root "is
  gitignored", and `templates/PR-DESCRIPTION.md` says the same. The
  `.gitignore` at ce59c8f lists five patterns and `PR.md` is not one of
  them, so an adopter who takes the sentence at its word commits the draft.

An adopter reading the template and the lifecycle side by side is given two
procedures and told to follow both; the one enforced by nothing is the one
dropped, as the lifecycle says of conventions that cannot both be followed.

## Specification

Documentation changes only. The template's instructions agree with the
lifecycle; the template's structure does not change.

### Files

- `templates/TICKET.md`
- `templates/PR-DESCRIPTION.md` — the `PR.md` sentence only
- `.gitignore` — only if the `PR.md` claim is kept rather than reworded

### Public surface

The templates are the surface an adopter copies; their instructions are
what an adopter does.

### Behaviour

- Step 5 names a branch whose name begins with the ticket identifier and
  does not name `master`.
- Step 1's id lookup matches the lifecycle's "Lineage" section, or points
  at it instead of restating it.
- The `PR.md` sentence is true of this repository: either `.gitignore`
  ignores `PR.md`, or the sentence says the adopting project ignores it.
- No rule is added; this ticket carries no falsifier of its own.

## Acceptance criteria

1. AC1: `grep -n "master\|docs/ticket-PRJ" templates/TICKET.md` returns
   nothing.
2. AC2: The id lookup in `templates/TICKET.md` and the one in
   `docs/ticket-lifecycle.md`, "Lineage", give the same next id on this
   repository's history.
3. AC3: `PR.md` is either matched by `.gitignore` or not claimed to be.
4. AC4: No template's structure or section list changes.

## Out of scope

- Any further reference repointing; EM-018 did that.
- Changing what the lifecycle says; the template follows the lifecycle,
  not the other way round.

## References

- `docs/ticket-lifecycle.md`, "Claiming" and "Lineage".
- `docs/ai-contributor-policy.md`, §7.
- EM-018 — the ticket this was found under.

## Notes

Proposed `standard` for the reason EM-018 gives: the change alters
instructions an adopter follows, and EM-007-002 owns the disagreement
between that reading and the operative test's `trivial` line.

## PR Description

> Leave this section empty when authoring the ticket.
