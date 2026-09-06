---
id: EM-012-001-001
title: The batch entry's supporting answer is still the standard-tier answer
status: done
tier: trivial
complexity: S
dependencies: [EM-012-001]
claimed_by: claude-fable-5-1
claimed_at: 2026-09-06
closed_at: 2026-09-06
---

# EM-012-001-001 — The batch entry's supporting answer is still the standard-tier answer

## Context

Raised by the independent review of EM-012-001 (finding R1.2 of round 1),
routed here under the second condition of "When review ends" because the
file lies outside EM-012-001's Files. `docs/ticket-lifecycle.md`, "Batching
trivial work", tells the holder that each entry records "its tier and the
operative-test answer that supports it — no clause holds". After EM-012-001
the answer that supports `trivial` is two-part: no clause holds, and
nothing a program executes or a caller reads as a contract is touched. As
written, an entry supported by the `standard` answer alone is a true
statement.

## Specification

Documentation change only.

### Files

- `docs/ticket-lifecycle.md` — "Batching trivial work", the second bullet.

### Public surface

N/A — this repository publishes documents. One clause is completed to
match the rule it cites.

### Behaviour

- The bullet reads: its tier and the answer that supports it — no clause
  holds, and nothing a program executes or a caller reads as a contract is
  touched.

## Acceptance criteria

1. AC1: the bullet states the two-part answer.
2. AC2: nothing else in the section changes.

## Out of scope

- Any change to the batch rule beyond the clause.

## References

- EM-012-001 — the test the clause now cites.
- `docs/ticket-lifecycle.md`, "Batching trivial work".

## Notes

Trivial: one clause completed; no procedure changes.

## PR Description

### Ticket
EM-012-001-001 — The batch entry's supporting answer is still the
standard-tier answer

### Tier
`trivial` — one clause completed to match the rule it cites; no procedure
changes. Self-merged, per the tier table. Re-tested at claim: the clause
adds words to a line every batch holder writes, but changes what the line
must say, not what the holder must do; the executor did not raise it.

### Summary
The batch rule's second bullet states the two-part answer that supports a
`trivial` entry.

### Acceptance criteria
- [x] AC1: the bullet states the two-part answer — `docs/ticket-lifecycle.md`,
  "Batching trivial work", second bullet.
- [x] AC2: nothing else in the section changes — `git diff HEAD~2..HEAD --
  docs/ticket-lifecycle.md` shows one bullet.

### Falsification
N/A — no behavioural claim. A batch holder writes the answer that actually
supports `trivial`, not the `standard` answer.

### Out of scope (per ticket)
Confirmed.

### How to verify
`grep -n "reads as a contract" docs/ticket-lifecycle.md docs/tier-review-model.md`
— the same phrase in the rule and in the entry line.

### Risks / follow-ups
None.

### Review
N/A — trivial tier.

