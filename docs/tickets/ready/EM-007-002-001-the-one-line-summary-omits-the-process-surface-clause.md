---
id: EM-007-002-001
title: The operative test's one-line summary omits the process-surface clause
status: ready
tier: standard
complexity: S
dependencies: [EM-007-002]
---

# EM-007-002-001 — The one-line summary omits the process-surface clause

## Context

Raised while working EM-007-002, under the contributor policy's §4.

`docs/tier-review-model.md`, "The operative test", closes with a summary
introduced by "In one line":

> **Could an existing caller, or a seeded run, notice this change without
> opting in? If yes, `critical`. If no, `standard` — or `trivial`, where
> nothing a program executes or a caller reads as a contract is touched.**

Its `critical` limb carries clauses 1 to 4 and not clause 5. A schema
migration, a CI configuration change and a change to the review model are
`critical` by clause 5, and no existing caller or seeded run notices any of
them, so the summary sends all three to `standard` or `trivial`.

This is visible on this repository rather than hypothetical. EM-007-002
writes into the same section the line that decides when a change to a
process document is `critical` — when it adds, alters or retires a rule or
a procedure — and that line hangs off clause 5. A contributor who runs the
summary instead of the clauses gets `trivial` for a rule change, which is
the answer the section now spends a page refusing.

The summary was already repaired once, by EM-012-001: round 1, finding
R1.3, a second-column finding its Review section records as "the one-line
summary refusing trivial to every documentation change". The remedy added
the `trivial` outcome. The `critical` limb was not in that finding's scope.

## Specification

Documentation change only.

### Files

- `docs/tier-review-model.md` — "The operative test", the block quote
  introduced by "In one line".

### Public surface

N/A — this repository publishes documents. One summary is made to agree
with the clauses it summarises.

### Behaviour

- The summary's `critical` limb returns `critical` for a change any of the
  five clauses catches, clause 5 included, so that a contributor who reads
  only the summary gets the same tier as one who runs the clauses.
- The five clauses are unchanged; this ticket edits the summary of them.
- No new rule is added, so no new falsifier is stated: the summary retires
  with the **Retired when:** line already beneath it.

## Acceptance criteria

1. AC1: the summary, read without the clauses above it, returns `critical`
   for a CI configuration change and for a change that adds a rule to a
   process document.
2. AC2: the summary still returns the same tier as the clauses for the
   changes it already answered correctly, and stays one sentence a
   contributor can hold.
3. AC3: the five clauses, the `trivial` line, and the process-document
   paragraph are unchanged.
4. AC4: an independent agent reviews this and records findings in two
   columns.

## Out of scope

- The five clauses.
- The `trivial` line and the process-document paragraph beneath it.
- What any tier requires.

## References

- `docs/tier-review-model.md`, "The operative test".
- EM-012-001 — the ticket that last repaired this summary, and its round-1
  record.
- EM-007-002 — the ticket this was raised under, which adds the paragraph
  that makes the omission load-bearing.

## Notes

Proposed `critical` when raised, under the paragraph EM-007-002 then added
to this same section.

**Read against the maintainer's answer to EM-007-002, 2026-09-10.** A change
to a process document is now `standard` on one independent pass, neither
`trivial` nor `critical`, and the tier is not raised; the frontmatter says
`standard` for that reason. What the answer moots: the Context's second and
third paragraphs, which motivate this ticket from the `critical`/`trivial`
line, which never landed; and the second half of AC1, since the summary's
process-document limb is written by EM-007-002 — "A process document is
`standard`, on one pass, whatever the answer." What stands, and is this
ticket: the summary's `critical` limb carries clauses 1 to 4 and not clause
5, so a contributor reading only the summary gets `standard` for a CI
configuration change and a schema migration, which clause 5 makes
`critical`. AC1 is read as its first half; AC3's "process-document
paragraph" is the one EM-007-002 lands; AC4 is the one pass.

## PR Description

> Leave this section empty when authoring the ticket.
