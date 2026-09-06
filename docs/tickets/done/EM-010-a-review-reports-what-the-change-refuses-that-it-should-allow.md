---
id: EM-010
title: A critical-tier review answers two questions, and over-tightening is a finding
status: done
tier: critical
complexity: S
dependencies: []
claimed_by: claude-fable-5-1
claimed_at: 2026-09-06
closed_at: 2026-09-06
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

## What this refuses, and what it costs

> Added 2026-09-05 on review of the wave, applying EM-010's two questions to the ticket that proposes them. A figure measured here names its baseline in the same sentence; a figure from a private project names the ticket section it is taken from; an assumption says so. Raised alongside EM-014; corrected after independent review of c0111ae.

**Refuses.**

- A first-column finding whose remedy cannot be costed. A new refusal on a
  path nothing has touched yet has a historical cost of zero commits and an
  unknown forward cost. The rule as written calls that finding incomplete, and
  an incomplete finding of a real hole may be dropped. What "cannot be
  measured" is allowed to look like is not defined here; the closest honest
  reading is that a stated population and a zero is a measurement and
  "unknowable" is not, and whether to write that into Behaviour is the
  maintainer's call.
- Reviewer severity judgement, by design, and the Notes say why.

**Costs.**

- Every critical-tier review is now two passes, and every tightening finding
  carries a measurement the reviewer must run — commit counts against a
  branch, or equivalent. On the source ticket's item 6 the result is recorded
  as 5 of 203 commits, per this ticket's Context; how it was obtained is not
  recorded. The cost is not the query, it is that the reviewer must know to
  make it, which puts the measurement in the brief.
- **Two-column ping-pong.** Column 1 tightens a rule; column 2 finds the
  tightening refuses honest work and loosens it; the next round tightens it
  again. EM-007's cap catches this after three rounds. Nothing catches it in
  round two when the ping-pong pair is a minority of the round; EM-007's own
  repairs-of-repairs signal fires when it is the majority. That is a gap in
  this ticket's design, and the fix is a stopping trigger — a specification
  change with a cost. It is raised as EM-014-001, from the review of the
  commit that added this section, rather than proposed here, because a
  change to Behaviour belongs in a ticket's own Specification with its cost
  stated, not in a paragraph the implementer cannot tell is in scope.

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

### Ticket
EM-010 — A review reports what the change refuses that it should allow

### Tier
`critical` — process-surface change (clause 5): it changes the reviewer's
brief and the review record.

**Independent review obtained**, per ADR-0002: a separate agent, given the
ticket, the diff and the two questions, and not the executor's reasoning,
reviewed the change in two rounds, read-only. Findings are under
Review; the tree was checked clean after each round.

### Summary
The tier review model gains "What a review reports", between the reviewer
section and "When review ends": the two questions, the equal rank of a
second-column finding, the reasoning in the model's own terms, OMN-021's
three named over-tightenings, and the rule that a tightening states its
cost in the same finding. The statement of what the reviewer receives now
includes the evidence and the two questions. The pull-request template's
Review section records findings per round in the two columns. One child
ticket raised, and it is the first id taken under the next-id-from-history
rule.

### Acceptance criteria
- [x] AC1: the two questions in their own section —
  `docs/tier-review-model.md`, "What a review reports", the numbered pair.
- [x] AC2: a second-column finding is a must-fix of equal rank — the bold
  sentence following, with the clarification that the column does not
  decide whether a finding blocks merge.
- [x] AC3: a tightening carries its cost in the same finding — the
  paragraph beginning "**A tightening states its cost.**"
- [x] AC4: what the reviewer receives includes the two questions — "Why
  'another agent, human or AI'", first sentence of its second paragraph,
  and the section's closing paragraph.
- [x] AC5: the template's Review section records findings in the two
  columns — `templates/PR-DESCRIPTION.md`, the per-finding lines after the
  per-round table.
- [x] AC6: every quoted figure names its source in the same sentence — the
  three over-tightenings carry "its pull-request description's
  over-tightening paragraph"; the 5-of-203 figure carries "counted in
  OMN-021-001, item 6" and its population.
- [x] AC7: independent review — see Review.

### Falsification
N/A — no behavioural claim. What a reader does differently, per criterion:
- AC1: a reviewer asks the second question in the round that introduces an
  over-tightening, instead of the next reviewer finding it incidentally.
- AC2: an executor repairs an over-tightening before merge instead of
  leaving it as the safe default.
- AC3: a reviewer proposing a list entry or an escalation writes, in the
  finding, which changes now pay it.
- AC4: whoever briefs a reviewer includes the evidence and the two
  questions, and a reviewer handed only the ticket and the diff knows the
  brief is short.
- AC5: a closing executor records findings by column, with cost beside each
  tightening, instead of in free prose.
- AC6: a reader can reach each figure's source without this ticket.

### Out of scope (per ticket)
Confirmed: the operative test is untouched; the stopping rule is untouched
(the new section sits before it and the two read in sequence); the measure
of cost is given as an example and not prescribed. The point the ticket's
Refuses section reserves to the maintainer — what "cannot be measured" may
look like — is not decided: the text says "measured where it can be
measured" and "incomplete" and defines neither.

Recorded, not fixed, on the reviewer's note: neither the model nor the
template says what the two questions mean for a documentation-only change,
which is most work here. The two closed records answer it by practice —
column 2 has held "the placement rule named no actor" and "an obligation
with no way to discharge it" — and a sentence saying so would widen the
section the ticket did not ask to widen.

### Review
| Round | Must-fix | Where (rules / lists / documents / tests) | Inside previous round's fix | Repaired by |
|---|---|---|---|---|
| 1 | 1 (of 7 findings) | documents: "a must-fix of the same rank" read two ways against the definition in "When review ends" (must-fix); "must-fix" used ahead of its definition; the columns' location unstated; the template's cost line unconditional; the 5-of-203 figure named the ticket, not the item; ADR-0002 lags the model (raised as EM-010-002); the two questions for a documentation-only change unstated | — | 7ad68a0 |
| 2 | 0 (of 1 note) | documents: a ragged paragraph left by the round-1 repair | 1 of 1 | the closing commit |

Derived total: 1 must-fix over two rounds. Findings by column,
round 1 — refuses: the equal-rank sentence's second reading would have made
every over-tightening note block merge, which the section itself says is the
defect (remedy: the column does not decide whether a finding blocks merge;
no cost); the definition ahead of first use; the columns' location; the
unconditional cost line. Permits: the item-6 source omitted; ADR-0002
lagging the model. Round 2 found no must-fix and one note inside the round-1 repair, re-flowed at close; it verified the EM-010-002 id claim against history. Post-review tree check after each round:
`git status --porcelain` empty, `git worktree list` showing only the main
tree.

### How to verify
1. `grep -n "^## " docs/tier-review-model.md` — "What a review reports"
   sits between the reviewer section and "When review ends".
2. `git diff ccb7823..HEAD -- docs/tier-review-model.md` — one new section
   and one amended sentence in the reviewer section; nothing else changed.
3. `git log --diff-filter=A --name-only --format= -- docs/tickets | grep
   EM-010-` — shows `EM-010-001` (spent) and `EM-010-002` (this branch).
4. `wc -w docs/tier-review-model.md templates/PR-DESCRIPTION.md` — at
   ccb7823: 1,549 and 630; at close: 2,110 and 709, as the reviewer measured at 7ad68a0.

### Risks / follow-ups
- **EM-010-002** (raised here): ADR-0002 lags the model on what the
  reviewer receives. Its id is the first taken under the
  next-id-from-history rule, because `EM-010-001` is spent.
- The two-column ping-pong the ticket's Costs section names is EM-014-001's.
- Every critical-tier review here is now a two-pass brief; this ticket's
  own review cost that, and the reviewer measured the model's growth at
  +524 words on this section alone.

