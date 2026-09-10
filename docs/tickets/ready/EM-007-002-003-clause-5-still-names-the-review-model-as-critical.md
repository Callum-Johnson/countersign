---
id: EM-007-002-003
title: Clause 5 of the operative test still names a change to the review model as critical
status: ready
tier: standard
complexity: S
dependencies: [EM-007-002]
---

# EM-007-002-003 — Clause 5 still names the review model as critical

## Context

Raised while working EM-007-002, under the contributor policy's §4, from
the one independent pass on that ticket (finding R5.2). Clause 5 of "The
operative test" in `docs/tier-review-model.md` — "A schema migration, a CI
configuration change, or a change to the review model itself" — sits under
the heading "Any one clause means `critical`", while the paragraph beneath
the test, landed by EM-007-002 under ADR-0004, makes a change to the review
model `standard` on one pass, the review model being a process document.
The two are reconciled only by the paragraph's own sentence claiming
precedence over the clause; a contributor who reads the clauses and stops
gets `critical`. EM-007-002's Out of scope excluded any change to the five
clauses, so the contradiction is left in the clause's words and this ticket
takes it.

## Specification

Documentation change only. `docs/tier-review-model.md`, "The operative
test", clause 5: amend its words so that they no longer name a change to
the review model, or so that they send such a change to the paragraph that
decides it, leaving a schema migration and a CI configuration change
`critical` as they are. No new rule is added; the clause retires with the
line already beneath the test. EM-007-002-001 works the one-line summary's
`critical` limb; this ticket works the clause, and the two do not overlap.

## Acceptance criteria

1. AC1: clause 5, read on its own, no longer returns `critical` for a
   change to the review model itself.
2. AC2: a schema migration and a CI configuration change still return
   `critical` under clause 5.
3. AC3: the paragraph beginning **A change to a process document** is
   unchanged, and its precedence sentence over clause 5 is either removed as
   no longer needed or left agreeing with the clause's new words.
4. AC4: one independent review pass, recorded as one row of the Review
   table, per "The operative test".

## Out of scope

- Clauses 1 to 4.
- The process-document paragraph and what any tier requires.
- The one-line summary, which is EM-007-002-001.

## References

- `docs/tier-review-model.md`, "The operative test", clause 5 and the
  paragraph beneath the test.
- ADR-0004, Consequences, the neutral bullet naming this clause.
- EM-007-002, Review, R5.2 — the finding this ticket is raised from.

## Notes

N/A

## PR Description

> Leave this section empty when authoring the ticket.
