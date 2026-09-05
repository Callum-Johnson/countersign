---
id: EM-007
title: State when an independent review ends
status: ready
tier: critical
complexity: S
dependencies: []
---

# EM-007 — Review terminates: a stopping rule for independent review

## Context

`docs/tier-review-model.md` says who reviews critical-tier work, what the
reviewer receives, and what the reviewer must do. It does not say when review
stops. The omission looks harmless because a review usually ends when a round
returns clean. It is not harmless where a round cannot return clean, and one
class of change guarantees that: an enumeration maintained against an
adversary — a list of paths, names or shapes that a control must catch. A
reviewer briefed to find the entry the list is missing will find one, every
round, because the list is finite and the adversary's options are not.

The evidence is one ticket on the control-plane project that implements this
process mechanically. OMN-021, a critical-tier governance change, went through
fourteen independent review rounds. Its own Review section records the
must-fix count per round — 7, 5, 2, 3, 4, 2, 2, 2, 6, 5, 3, 1, 2, 2 — which sums
to 46, and records how many of each round's findings sat inside the previous
round's own repair — 1, 2, 3, 3, 2, 2, 2, 3, 4, 3, 0, 2, 2 for rounds 2 to 14 —
which sums to 29. So 29 of the 46 must-fixes on that ticket, derived from the
per-round figures in its Review section, were defects in a fix rather than in
the original work. The eight rules the ticket built were unchanged after round
6; every finding from round 7 to round 14 was in two path lists. The branch's
commit timestamps show the claim at 05:51, the feature commit at 06:01 and the
fourteenth repair at 17:47 on 2026-09-04: ten minutes building, and the rest of
the day reviewing and repairing without a rule that could have said stop.

"Every round found something" was read throughout as the review earning its
keep. Under this model's own reasoning it is the opposite: a process with no
statement of what a converged review looks like cannot be shown to have
converged, only to have been stopped. The falsification gate makes the same
demand of a test — name the thing that would make it fail — and it applies to
the review process as much as to the code the process reviews.

The record also shows what a stopping rule would have done. From round 7 the
ticket had already recorded, as a stated narrowing with its own child ticket,
that the gate it re-runs executes the branch's own toolchain, and every list
finding after that was an instance of that one recorded limit. A rule that
routes findings inside a recorded limit to the ticket that owns the limit would
have ended the loop at round 7 with the same eight rules.

## Specification

Documentation changes only.

### Files

- `docs/tier-review-model.md` — a new section, "When review ends", after
  "Why 'another agent, human or AI'".
- `templates/PR-DESCRIPTION.md` — a `### Review` section for critical-tier
  work, carrying the per-round record the stopping rule reads.
- `docs/ai-contributor-policy.md` §3 — one sentence cross-referencing the new
  section, so that a reader of the blocking rule learns that non-convergence
  is one of its triggers.

### Public surface

N/A — this repository publishes documents. The surface is the set of rules a
reader may have adopted, and this ticket adds to that set without changing an
existing rule.

### Behaviour

- The section states three conditions under which a review round ends the
  loop **without a further fix**, and names where each condition's findings
  go:
  1. The round finds no must-fix. Review is complete.
  2. Every must-fix in the round lies inside a limit the ticket already
     records — an out-of-scope item, a stated narrowing, a child ticket. The
     findings go to the ticket that owns the limit, raised if it does not
     exist. Review of this ticket is complete with the limit recorded at full
     strength in the pull-request description.
  3. Every must-fix in the round adds an entry to an enumeration the change
     maintains against an adversary. The entries are added once, the list is
     recorded as best-effort with the review's coverage stated, and further
     rounds against the list are list-building rather than review. A finding
     that adds an entry to a list is evidence the list is a list, not evidence
     the rules are wrong.
- The section states a maximum number of rounds a single ticket may take
  before it blocks to the maintainer with its review record, and states that
  this block is a success path in exactly the sense of the contributor
  policy's §3: the executor has correctly identified that the loop is not
  converging, and the alternative is another round that looks like progress.
  A default of three rounds is named as a default, with the reasoning that on
  the source ticket rounds 1 to 3 found the rules' defects and everything
  after was lists.
- The section states the signal for a loop that is repairing its own repairs:
  when a round's must-fixes are mostly inside the previous round's fix, the
  next step is not another per-finding repair but a redesign of the fix
  against its class. The mechanism for that is EM-009 and is referenced, not
  restated.
- The `### Review` section of the pull-request template records, per round:
  the round number, the must-fix count, where the findings sat (rules, lists,
  documents, tests), how many sat inside the previous round's fix, and the
  commit that repaired it. **The total is derived from the per-round figures
  and never asserted beside them.** The source ticket's total drifted three
  times — recorded in its own Review section as "sixteen", "thirty-five" and
  "twenty-nine" — while it was asserted rather than derived.

## What this refuses, and what it costs

> Added 2026-09-05 on review of the wave, applying EM-010's two questions to the ticket that proposes them. A figure measured here names its baseline in the same sentence; a figure from a private project names the ticket section it is taken from; an assumption says so. Raised alongside EM-014; corrected after independent review of c0111ae.

**Refuses.**

- A fourth round on a ticket whose third round still found rule defects. The
  three conditions exist to prevent exactly that, but the cap applies whether
  or not the conditions were applied, and where they were not, the cap ends
  the wrong review. The cap's own falsifier, stated so it can be watched for: a
  ticket blocked at cap whose maintainer, reading the record, orders a further
  round that finds a rule defect.
- A reviewer's judgement that a list is dangerously incomplete. Condition 3
  ends list review after one round of additions and records coverage. A
  reviewer convinced the list is short has that one round to say so.

**Costs.**

- The per-round record: five fields per round in every critical-tier
  pull-request description. On OMN-021 that is fourteen rows, one per round
  in the per-round counts its Review section records and this ticket's
  Context quotes; on a one-round review it is one. The template carries nine
  `###` headings today, measured 2026-09-05 at 8b0a8b4 — seven template
  sections inside the code block and two document headings; this ticket adds
  one template section, and EM-009 adds another.
- Each block at cap costs a maintainer read of the review record and a
  decision. On the source ticket the saving is eleven rounds against one
  block. On a project with several non-converging tickets at once, the
  maintainer becomes the bottleneck the block was meant to protect; the rule
  should say what the maintainer does with three blocked records in a day.

## Acceptance criteria

1. AC1: `docs/tier-review-model.md` states, in its own section, the conditions
   under which a review round ends the loop without a fix, and for each
   condition names where the findings go.
2. AC2: The section states a maximum round count with a named default and its
   reasoning, and states that blocking on non-convergence is a success path,
   cross-referencing the contributor policy's §3.
3. AC3: The section states that a finding which adds an entry to an
   enumeration does not reopen review of the rules the enumeration serves.
4. AC4: `templates/PR-DESCRIPTION.md` carries a `### Review` section with the
   per-round fields above, and states that the total is derived, not asserted.
5. AC5: `docs/ai-contributor-policy.md` §3 names non-convergence as a trigger
   for the blocking procedure, in one sentence, without restating the rule.
6. AC6: The source ticket's figures, where quoted, name the section they are
   derived from in the same sentence, per the baseline rule EM-006 introduces.
7. AC7: Critical tier per ADR-0002: an independent agent that did not perform
   the work reviews this against the artifacts and records findings in the
   pull-request description.

## Out of scope

- Tuning the round cap from evidence. Three is a default named as one; a
  measured value needs more than one ticket's record and is a later change.
- The class-repair obligation. EM-009.
- The two-column review report. EM-010.
- Any change to who reviews or what the reviewer receives.

## References

- `docs/tier-review-model.md` — the section this ticket extends.
- `docs/ai-contributor-policy.md` §3 — blocking as a success path, which this
  ticket gives a second trigger.
- ADR-0002 — the countersignature requirement this ticket bounds.
- EM-006 — the falsification gate, whose demand this ticket makes of the
  review process itself; and its baseline rule, which the figures above follow.
- OMN-021 on the control-plane project — the Review section of its ticket and
  the commit timestamps on its branch are the evidence quoted above.

## Notes

**Why a stopping rule is not a cap alone.** A cap without the three
conditions ends a review that is still finding rule defects, which is the
wrong review to end. The conditions end the review that cannot converge; the
cap catches the case where nobody applied them.

**Working this with EM-008 to EM-011.** The five tickets raised from the same
evidence are separable and each is a decision the maintainer may take or
decline on its own, which is why they are five. They may be worked as one
wave and reviewed together, and the reviewer should be told they are one
wave so that the review's own record can be kept per the format this ticket
introduces.

**This ticket's own gates.** As EM-006 says of itself: for each acceptance
criterion, the reviewer should be able to say what a reader would do
differently because of the change. For this ticket the reader is an executor
at the end of a review round, and the thing done differently is that a round
whose findings are all inside a recorded limit produces a ticket and not a
fifteenth fix.

## PR Description

> Leave this section empty when authoring the ticket.
