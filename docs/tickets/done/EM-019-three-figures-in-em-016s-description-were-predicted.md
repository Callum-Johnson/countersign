---
id: EM-019
title: Three figures in EM-016's closed description were predicted, not measured
status: done
tier: trivial
complexity: S
dependencies: []
claimed_by: claude-fable-5-1
claimed_at: 2026-09-06
closed_at: 2026-09-06
---

# EM-019 — Three figures in EM-016's description were predicted, not measured

## Context

Found on 2026-09-06, immediately after EM-016 merged at 858fcbb, by running
`wc -w` against the figures its own description asserts.

EM-016's pull-request description states the word count of
`docs/ai-contributor-policy.md` at close as 2,899, the five-document total
as 12,305, and the change's own addition as 822 words. Measured at 858fcbb
the three are 2,897, 12,303 and 820. The error is two words in each, and it
has one cause: the closing commit took a review note that added five words
to the map, and the figures were written from an estimate of that edit
rather than measured after it.

This is the defect EM-006 exists to name, in the repository that names it.
Its Notes say a measured number and an inherited one are indistinguishable
once written down; a predicted one is worse, because the writer knows the
measurement was available. The contributor policy's §6 requires the
baseline in the same sentence, which the description gives correctly; what
it does not do is require the number to have been taken after the last
edit, and nothing catches that but measuring again.

## Specification

Documentation change only.

### Files

- `docs/tickets/done/EM-016-bound-the-brief-a-contributor-must-read.md`

### Public surface

N/A — this repository publishes documents. No rule changes; three figures
in a closed record are corrected and the correction is shown.

### Behaviour

- The three figures read 2,897, 12,303 and 820.
- The correction is visible in the record rather than silent: a dated line
  states what the figures said, what they say now, and how they came to be
  wrong. A closed description edited without a mark is a record a reader
  cannot trust.
- The derived figures that depend on them are checked and corrected with
  them, or confirmed unaffected.

## Acceptance criteria

1. AC1: `wc -w` on the five rule-bearing documents at close matches every
   figure in EM-016's description.
2. AC2: the description carries a dated line recording the correction and
   its cause.
3. AC3: no other text in the closed description changes.

## Out of scope

- Any change to the documents EM-016 edited. The figures were wrong; the
  change they describe was not.
- Any rule about when a figure is measured. If one is wanted — that a
  description's figures are taken after the last commit that changes them —
  that is a rule with a cost and its own ticket.

## References

- EM-016 — the description corrected here.
- EM-006, Notes — "a measured number and an inherited one are
  indistinguishable once written down", the rule this instance breaks.
- `docs/ai-contributor-policy.md` §6 — the baseline requirement, which the
  description met and which did not catch this.

## Notes

Trivial by the operative test: no clause holds, and nothing a program
executes or a caller reads as a contract is touched — a closed ticket file.

## PR Description

### Ticket
EM-019 — Three figures in EM-016's closed description were predicted, not
measured

### Tier
`trivial` — a closed ticket file; no clause of the operative test holds and
nothing a program executes or a caller reads as a contract is touched.
Self-merged, per the tier table.

### Summary
The three figures read 2,897, 12,303 and 820, and a dated line in the same
section records what they said, what they say now, and why they were wrong.

### Acceptance criteria
- [x] AC1: every figure matches `wc -w` at close — the five documents
  measure 2,897, 4,461, 2,229, 2,153 and 563, totalling 12,303, and the
  change against baseline e1beeb6's 11,483 is 820.
- [x] AC2: the correction is dated, names this ticket, and gives the cause
  — "**Corrected 2026-09-06 under EM-019.**"
- [x] AC3: no other text changes — the diff is three figures, one inserted
  paragraph, and one repeated figure in the prose beneath.

### Falsification
N/A — no behavioural claim. A reader checking EM-016's figures against the
tree now finds them, and a reader who noticed the discrepancy finds it
recorded rather than quietly gone.

### Out of scope (per ticket)
Confirmed: the documents EM-016 edited are untouched, and no rule about
when a figure is measured was added. That rule — a description's figures
are taken after the last commit that changes them — would have caught this
and has a cost; it is named in the ticket's Out of scope and not taken.

### How to verify
`wc -w docs/ai-contributor-policy.md docs/tier-review-model.md
docs/quality-gates.md docs/ticket-lifecycle.md docs/adr-process.md` against
the table in EM-016's description.

### Risks / follow-ups
The description satisfied §6 — every figure named its baseline — and was
still wrong, because §6 requires the baseline and not the measurement. Two
of the wave's own tickets state figures taken before their closing commits;
whether that rule is worth its cost is a decision for the maintainer, not
this ticket.

### Review
N/A — trivial tier.

