---
id: EM-010
title: A critical-tier review answers two questions, and over-tightening is a finding
status: ready
tier: critical
complexity: S
dependencies: []
---

# EM-010 — A review reports what the change refuses that it should allow

## Context

`docs/tier-review-model.md` briefs the critical-tier reviewer to verify the
evidence and run the suite. It says what the reviewer must not accept — the
executor's summary — and it says why independence matters. It does not say
what a finding is, and in practice a reviewer briefed to look hard looks for
one thing: what the change lets through that it should not. Nobody is asked
the other question, and so a review that runs for several rounds tightens
monotonically, because every finding adds a refusal and no finding removes
one.

The model already knows this is a defect. Its scrutiny-list section says that
an escalation everyone ignores is worse than none, because it trains
contributors to treat escalation as noise. A control that refuses honest work
is that escalation with teeth.

The evidence is OMN-021 on the control-plane project that implements this
process mechanically. Its pull-request description records that its review
produced over-tightening four times, and names three of the four with the
round that caught each:

1. A rule refused the board index every claim touches, which made **every
   branch in the repository** unmergeable. Caught in round 4, one round after
   it was written.
2. A rule denied on inherited duplicate identifiers, which stalled every
   branch in any corpus with a pre-existing collision. Caught in round 5.
3. A rule refused any non-Markdown file under the ticket directory as another
   ticket's file, with no achievable remedy, while two such files sat on the
   branch. Caught in round 6.

Each was caught only by review, and each was caught a round late — by the
next reviewer, incidentally, while looking for holes. A reviewer asked "what
does this refuse that it should allow" would have found the first one in the
round that introduced it, because the answer was every branch including the
one under review.

The same asymmetry shapes the remedy of a genuine hole. A reviewer who finds
that a list is missing an entry proposes the entry; nobody at that moment
prices what the entry costs. On the source ticket a configuration filename
was added to a list that raises the review tier of any change touching it,
matched anywhere in the tree; the file it matched at the repository's own
root is touched by 5 of the 203 commits on that repository's default branch,
counted by the ticket's own child OMN-021-001, and each of those would now
need an independent approval. The cost was measured after the fact, by the
executor, for the maintainer. It should have been in the finding.

## Specification

Documentation changes only.

### Files

- `docs/tier-review-model.md` — a new section, "What a review reports", or an
  extension of "Why 'another agent, human or AI'".
- `templates/PR-DESCRIPTION.md` — the `### Review` section EM-007 introduces
  gains the two columns; if EM-007 has not landed, this ticket introduces the
  section with only the columns and EM-007 adds the per-round record.

### Public surface

N/A — this repository publishes documents. The change adds to the reviewer's
brief and removes nothing from it.

### Behaviour

- The model states that a critical-tier review answers two questions of the
  change, and records the answers as two columns of findings:
  1. **What does the change permit that the ticket says it must refuse?**
  2. **What does the change refuse that honest work needs?**
- A finding in the second column is a must-fix of the same rank as a finding
  in the first. Over-tightening is a defect, not a conservative default.
- A finding in the first column whose remedy adds to a control — a list
  entry, a tier escalation, a refusal — states in the same finding what the
  addition costs: which ordinary changes now pay the control, measured where
  it can be measured. A finding that cannot say what its remedy costs is
  incomplete.
- The reviewer receives the two questions as part of the brief, alongside the
  ticket, the diff and the evidence. The model's statement of what the
  reviewer receives is amended to say so.
- The reasoning is stated in the model's own terms: a control the controlled
  party ignores is not a control, and a review that only ever tightens
  produces controls that get ignored.

## Acceptance criteria

1. AC1: `docs/tier-review-model.md` states the two questions every
   critical-tier review answers, in its own section or as a named extension of
   the existing reviewer section.
2. AC2: The model states that a second-column finding is a must-fix of equal
   rank with a first-column finding.
3. AC3: The model states that a first-column finding whose remedy tightens a
   control carries the cost of the tightening in the same finding.
4. AC4: The statement of what the reviewer receives includes the two
   questions.
5. AC5: `templates/PR-DESCRIPTION.md`'s Review section records findings in
   the two columns.
6. AC6: The source ticket's figures, where quoted, name the section they are
   derived from in the same sentence.
7. AC7: Critical tier per ADR-0002: an independent agent that did not perform
   the work reviews this against the artifacts and records findings in the
   pull-request description.

## Out of scope

- Any change to the tier model's operative test. It performed correctly on
  the source ticket; the tier was right, and the reviews were the right
  reviews at the wrong brief.
- The stopping rule. EM-007.
- Prescribing how cost is measured. Commit counts against a default branch
  are one measure and are given as an example.

## References

- `docs/tier-review-model.md` — the scrutiny-list section, whose reasoning
  this ticket applies to review findings; and the reviewer section this ticket
  extends.
- EM-007 — the Review section of the pull-request template that this ticket
  shares.
- OMN-021 on the control-plane project — its pull-request description's
  over-tightening paragraph, and OMN-021-001 item 6 for the measured cost.

## Notes

**Why two columns and not a severity.** A severity scale asks the reviewer to
rank a hole against an over-tightening, which reintroduces the judgement the
two questions exist to separate. Two columns of equal rank make the reviewer
answer both questions; what to do about the answers is the executor's and
the maintainer's.

**Working this with EM-007 to EM-009 and EM-011.** See EM-007's Notes.

## PR Description

> Leave this section empty when authoring the ticket.
