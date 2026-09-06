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

### Ticket
EM-016-001-001 — The README's fourth core idea names two tiers of three

### Tier
`trivial` — one sentence in `README.md`; no clause of the operative test
holds and nothing a program executes or a caller reads as a contract is
touched. No independent review at this tier; the author self-merges, per
the tier table.

### Summary
Core idea 4 of `README.md` now states the operative test as the tier
review model's one-line form states it: yes means critical and a second
reviewer; no means standard — or trivial, where nothing a program executes
or a caller reads as a contract is touched. The idea stays one paragraph
and restates no more of the model than it did.

### Acceptance criteria
- [x] AC1: `README.md`, core idea 4, names three tiers and the line that
  separates `trivial` from `standard`, in the terms
  `docs/tier-review-model.md`, "The operative test", uses — the idea now
  reads "No means standard — or trivial, where nothing a program executes
  or a caller reads as a contract is touched"; the model's one-line form
  reads "or `trivial`, where nothing a program executes or a caller reads
  as a contract is touched". The three tier names appear in the idea in
  the model's order, critical first.
- [x] AC2: no other part of `README.md` changes — `git diff 9fd9a56 HEAD
  -- README.md` at 5de1922 shows 5 changed lines, 2 removed and 3 added,
  all within core idea 4; the lines wrapped before and after the changed
  sentence are as they were.

### Falsification
N/A — no behavioural claim. What a reader does differently, per criterion:
- AC1: a reader who starts at the README's core ideas and stops there
  learns that a documentation change is `trivial` and self-merges it
  without a review, rather than taking it as `standard` and writing
  evidence per criterion the tier does not ask for — or, having read the
  "Start here" row above that says three tiers, looking for a third the
  idea beneath did not name. The line that separates the two tiers is
  stated beside the tiers, not only in the model.
- AC2: nothing; it is the guard. A reader of any other part of the README
  finds it as EM-016-001 left it.

### Out of scope (per ticket)
Confirmed: no other core idea and no row of the "Start here" table
changes, and the operative test in `docs/tier-review-model.md` is
untouched — `git diff 9fd9a56 HEAD --stat` at 5de1922 lists `README.md`
beside the ticket file and the board only.

Left as it stands: the question the idea italicises says "a seeded roll"
where the model's one-line form says "a seeded run". The ticket's
Behaviour binds the answer to the model's form, not the question; the
question is the README's own register for the same clause, which the
Behaviour allows a summary to keep, and it sends no reader to a different
tier.

### How to verify
1. Read `README.md`, core idea 4, beside `docs/tier-review-model.md`,
   "The operative test", "In one line": the two agree on the three tiers
   and on what separates `trivial` from `standard`.
2. `git diff 9fd9a56 HEAD -- README.md` — 5 changed lines, all within
   core idea 4.

### Risks / follow-ups
- None raised. The idea now restates one more clause of the model than it
  did, and the map's same-commit rule does not bind the core ideas — the
  "Start here" row is what EM-016-001 bound. When the model's one-line
  form next changes, this sentence is a second place that must follow it
  by hand. EM-006-001 caught this shape against core idea 5 and this
  ticket against core idea 4; a further instance is the case for binding
  the core ideas as the table is bound.

### Review
N/A — trivial tier.
