---
id: EM-016-001-001
title: The README's fourth core idea names two tiers of three
status: in-progress
tier: trivial
complexity: S
dependencies: []
claimed_by: claude-fable-5-1
claimed_at: 2026-09-06
---

# EM-016-001-001 — The README's fourth core idea names two tiers of three

## Context

Raised while working EM-016-001, which brought `README.md`'s "Start here"
table up to what each document settles and put the README's core ideas out
of its own scope.

`README.md`, core idea 4, states the operative test in one line: "Yes means
critical and a second reviewer. No means standard." The test's own one-line
form in `docs/tier-review-model.md`, "The operative test", reads
differently as EM-012-001 leaves it: no means `standard` — or `trivial`,
where nothing a program executes or a caller reads as a contract is
touched. The "Start here" row above the core ideas now says three tiers;
the idea beneath it names two. This is the shape of finding EM-006-001
recorded against core idea 5.

## Specification

Documentation change only.

### Files

- `README.md` — core idea 4.

### Public surface

N/A — this repository publishes documents. One sentence is brought up to
the test it summarises; no rule changes.

### Behaviour

- Core idea 4 states the one-line test as the tier review model states it:
  yes means `critical` and a second reviewer; no means `standard`, or
  `trivial` where nothing a program executes or a caller reads as a
  contract is touched.
- The idea stays one paragraph and restates no more of the model than it
  does now.

## Acceptance criteria

1. AC1: `README.md`, core idea 4, names three tiers and the line that
   separates `trivial` from `standard`, in the terms
   `docs/tier-review-model.md`, "The operative test", uses.
2. AC2: no other part of `README.md` changes.

## Out of scope

- Any other core idea, and the "Start here" table (EM-016-001).
- Any change to the operative test itself.

## References

- `docs/tier-review-model.md`, "The operative test" — the one-line form,
  as EM-012-001 leaves it.
- EM-006-001 — the same shape of finding, against core idea 5.
- `README.md`, "The core ideas".

## Notes

Trivial by the operative test as EM-012-001 leaves it: one sentence in a
document no program executes and no caller reads as a contract. The tier
question EM-007-002 owns applies here as it does to every documentation
ticket on this board.

## PR Description

> Leave this section empty when authoring the ticket.
