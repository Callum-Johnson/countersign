---
id: EM-001-001-001
title: The lifecycle has no close for a ticket that will not be worked
status: ready
tier: standard
kind: defect
impact: degraded
delivery: maintenance
why: "Without a written close for a ticket that will not be worked, such a ticket either closes as done against the plain meaning of the word or stays in blocked/ indefinitely, and the board stops reporting what is true."
complexity: S
dependencies: []
claimed_by:
claimed_at:
blocked_at:
closed_at:
---

# EM-001-001-001 - The lifecycle has no close for a ticket that will not be worked

## Why this ticket should be worked

The affected outcome is the board's honesty, which ADR-0001 makes this
repository's own record of itself.

Deferring this degrades that record in a specific way. `done/` is defined by
the board as "Merged, with the pull-request description appended", and
"Closing" in the lifecycle describes a ticket that was worked: append the
description, set `closed_at`, move. A ticket the maintainer decides not to
work has none of that, and the invariant offers no fourth destination - so it
either sits in `blocked/` after its block has been answered, which reads as
"still waiting" to anyone scanning the board, or it takes `done/` and the word
means two things.

The evidence is EM-001-001, closed 2026-09-15. Its blocker was discharged not
by an answer but by a decision that the work would not happen, and it took the
`done/` path for want of another, saying so in its own Tier and Risks
sections. That is the workaround, and it is the reason this is `degraded`
rather than `feature-blocking`: the board still functions, and a reader who
opens the ticket learns the truth.

Deferral is acceptable until a second instance occurs. See Notes.

## Context

Raised while closing EM-001-001, whose Specification the maintainer declined
in full. Nothing in `docs/ticket-lifecycle.md` covers the case.

## Specification

Documentation change only.

### Files

- `docs/ticket-lifecycle.md`, "Closing".
- `docs/tickets/README.md`, the directory table, if a directory is added.

### Public surface

N/A - this repository publishes documents.

### Behaviour

- "Closing" states how a ticket closes when the maintainer decides the work
  will not be done: what the record carries in place of a pull-request
  description that demonstrates acceptance criteria, and which directory
  holds it.
- The clause states its falsifier.
- Whether this needs a fourth directory or a marked `done/` is the ticket's
  to decide, with the cost of each stated. A fourth directory changes the
  invariant, which is the more expensive of the two.

## Acceptance criteria

1. AC1: A second instance is named in Context, per "A rule needs a second
   instance". Until then this ticket is not worked - see Notes.
2. AC2: `docs/ticket-lifecycle.md` states the close for a ticket that will
   not be worked.
3. AC3: The clause carries a **Retired when:** line.
4. AC4: If a directory is added, `docs/tickets/README.md` and the
   directory/status invariant agree with it.
5. AC5: A change to a process document is `standard` on one independent
   review pass, per "The operative test"; the pass is recorded as one row of
   the Review table.

## Out of scope

- Reopening EM-001-001 or any other closed ticket.
- Any change to what `done/` means for a ticket that was worked.

## References

- `docs/ticket-lifecycle.md`, "Closing" - the procedure with the gap.
- `docs/tickets/README.md` - the directory table and the invariant.
- EM-001-001 - the first instance, and the workaround it took.
- `docs/tier-review-model.md`, "A rule needs a second instance" - the bar
  this ticket has not yet cleared.

## Notes

**Not claimable yet.** "A rule needs a second instance" bars a rule from
entering these documents until the failure is met a second time, in a second
ticket or on a second project. EM-001-001 is the first. This ticket is raised
now under the contributor policy's §4 so the first instance is recorded where
it was met, and it waits in `ready/` rather than `blocked/` because no
executor has claimed it and stopped; it is specified and merely premature.
An executor that picks it up before AC1 can be ticked should put it back.

## PR Description

> Leave this section empty when authoring the ticket.
