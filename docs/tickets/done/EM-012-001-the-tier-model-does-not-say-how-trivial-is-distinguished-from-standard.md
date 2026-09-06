---
id: EM-012-001
title: The tier model does not say how trivial is distinguished from standard
status: done
tier: critical
complexity: S
dependencies: [EM-012]
claimed_by: claude-fable-5-1
claimed_at: 2026-09-06
closed_at: 2026-09-06
---

# EM-012-001 — The tier model does not say how trivial is distinguished from standard

## Context

Raised by the independent review of EM-012 (finding R1.2 of round 1). The
operative test in `docs/tier-review-model.md` has two outcomes: any clause
holds, `critical`; none holds, `standard`. The tier table has three rows.
`trivial` is assigned only by the table's "Typical work" column —
documentation, comments, data additions, ticket edits — and nothing states
the test that separates it from `standard`. EM-012's batch path admits "a
change whose tier is `trivial`", and an adopter listing entries with "the
operative-test answer that supports it" can write only that no clause
holds, which is the `standard` answer too.

EM-012's Out of scope reserves "any change to the operative test, or to
what `trivial` means"; the gap is recorded here rather than closed there.

## Specification

Documentation change only.

### Files

- `docs/tier-review-model.md` — "The operative test" or "The tiers".

### Public surface

N/A — this repository publishes documents. The change states a test that
the table already implies.

### Behaviour

- The model states, in one or two sentences, the test that returns
  `trivial` where the operative test returns `standard`: a change that no
  code path executes and no contract reads — documentation, comments, data
  a program does not load, ticket files — is `trivial`; anything a program
  or a caller can observe is at least `standard`.
- The sentence says who decides where the line is unclear: the executor
  may raise, never lower, as the separation-of-duties section already
  says.
- The rule states its falsifier, per "Retiring a control". Stated here
  at close, since the ticket was claimed without it: retired when a change
  classed `trivial` under the sentence is found to have touched something a
  program executes or a caller reads as a contract, more than once over a
  stated population — closed batch tickets' recorded reclassifications, or
  a maintainer's spot-check of self-merged work.

## Acceptance criteria

1. AC1: `docs/tier-review-model.md` states a yes/no test for `trivial`.
2. AC2: The test is consistent with the table's "Typical work" column and
   changes no row's review requirement.
3. AC3: The rule carries a Retired-when line.
4. AC4: Critical tier per ADR-0002: an independent agent reviews this
   against the artifacts and records findings in two columns.

## Out of scope

- Changing what the operative test returns `critical` for.
- Changing any tier's review requirement.

## References

- `docs/tier-review-model.md`, "The operative test" and "The tiers".
- EM-012 — the batch path that needs the test, and its Out of scope.
- ADR-0001, Alternative 3 — "trivial-tier work needs a ticket but no
  review", which assumes the tier can be told.

## Notes

Critical under the operative test's process-surface clause: the tier model
is the review model.

## PR Description

### Ticket
EM-012-001 — The tier model does not say how trivial is distinguished from
standard

### Tier
`critical` — the tier model is a process surface (clause 5).

**Independent review obtained**, per ADR-0002: a separate agent, given the
ticket, the diff and the two questions, and not the executor's reasoning,
reviewed the change in two rounds, read-only. Findings are under
Review; the tree was checked clean after each round.

### Summary
The operative test's closing sentence gains the `trivial` test: a change
that touches nothing a program executes and nothing a caller reads —
documentation, comments, ticket files, data no program loads — is
`trivial`; anything a program or a caller can observe is at least
`standard`; where the line is unclear the executor may raise, never lower.
The rule states its falsifier, as a ticket raised after EM-014 closed must.

### Acceptance criteria
- [x] AC1: a yes/no test for `trivial` — `docs/tier-review-model.md`, "The
  operative test", the sentence beginning "If none hold, the tier is
  `standard` — unless".
- [x] AC2: consistent with the table's "Typical work" column and no row's
  review requirement changes — the column's four items (documentation,
  comments, data additions, ticket edits) are the sentence's examples, with
  "data additions" narrowed to data no program loads, since data a program
  loads is observable by a caller; the table is untouched.
- [x] AC3: the rule carries a Retired-when line — the paragraph following.
- [x] AC4: independent review, in two columns — see Review.

### Falsification
N/A — no behavioural claim. What a reader does differently, per criterion:
- AC1: an executor writes "no clause holds, and nothing a program executes
  or a caller reads is touched" as a batch entry's answer, instead of the
  `standard` answer for a `trivial` change.
- AC2: a reader of the table's "data additions" knows which data.
- AC3: a reviewer knows what evidence would retire the line.

### Out of scope (per ticket)
Confirmed: what the test returns `critical` for is unchanged; no tier's
review requirement changes.

### Review
| Round | Must-fix | Where (rules / lists / documents / tests) | Inside previous round's fix | Repaired by |
|---|---|---|---|---|
| 1 | 4 (of 7 findings) | documents: the table's trivial row wider than the test (must-fix); the one-line summary still two outcomes (must-fix); "observe" wider than "executes or reads", giving the sentence's own examples two answers (must-fix); the batch entry's supporting answer, outside Files, routed as EM-012-001-001 (must-fix discharged by raising); the falsifier's population and referent; the ticket claimed without its falsifier; README idea 4's two outcomes | — | 883d7b2 |
| 2 | 0 (of 2 notes) | documents: the definitional list reads as closed; the routed child's proposed tier | 1 of 2 | recorded |

Derived total: 4 must-fix over two rounds.
Round 1 by column and rule — permits: R1.1, the tier table's trivial row
(remedy: "data no program loads"; what now pays standard is data a program
loads, none of it on this board); R1.2, the batch rule's per-entry answer,
outside Files (routed under the second condition of "When review ends" to
EM-012-001-001, the must-fix discharged by raising it); R1.4, README idea
4's two outcomes (recorded, outside Files, for whichever ticket next
touches it); R1.5, the falsifier (remedy: its referent and two
populations named); R1.9, the ticket's own Behaviour promised a falsifier
and stated none — the ticket was claimed short of ready under ADR-0003's
clause, and the landed falsifier is now written into its Behaviour with
that said. Refuses: R1.3, the one-line summary refusing trivial to every
documentation change (remedy: the third outcome in the summary; a
loosening); R1.6, "observe" against "executes or reads", so that a ticket
file was trivial by one sentence and standard by the next (remedy: one
verb pair, defined once; a loosening). Round 2's two notes are recorded:
the definitional list reads as closed, and "code" is meant to carry
scripts, hooks and build files; EM-012-001-001's trivial tier follows the
precedent of EM-007-001 and EM-010-002 and the executor may raise it at
claim.
Post-review tree check after each round: `git status --porcelain` empty,
`git worktree list` showing only the main tree.

### How to verify
1. `grep -n "trivial" docs/tier-review-model.md` — the test in "The
   operative test", the table row, the batch pointer, the fifth-gate
   sentence.
2. `git diff 650f812..HEAD --stat` — one document and ticket
   housekeeping.

### Risks / follow-ups
- "Data no program loads" narrows the table's "data additions". Content
  files a program loads are `standard` under this sentence, which is the
  reading the operative test's determinism clause already implies.

