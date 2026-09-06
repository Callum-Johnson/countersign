# Tier review model

Every ticket declares a risk tier. The tier sets the minimum review required
before merge.

The point of the model is that the tier is decided by **the semantics of the
change, not the location of the file it lands in**. "This file is important,
so be careful" is not a control; it is a mood. What follows is a test with a
yes/no answer.

---

## The operative test

Run it against your change. **Any one clause means `critical`:**

1. **Contract change.** You alter, remove, or change the meaning of an
   existing field, function signature, or return shape, such that an existing
   caller could observe the difference. *Adding a new optional field that
   defaults to a no-op is not this.*
2. **Behaviour change to an existing caller.** Existing code resolves
   differently with no new opt-in. *A new branch reached only by new callers
   is not this.*
3. **Ordering change.** You change the sequencing of an existing state
   machine or reducer. *Adding an observer hook that nothing existing reads is
   not this.*
4. **Determinism.** You touch the seeded random source, seed threading, or
   anything that could change a reproducible outcome.
5. **Process surface.** A schema migration, a CI configuration change, or a
   change to the review model itself.

If none hold, the tier is `standard`. In one line:

> **Could an existing caller, or a seeded run, notice this change without
> opting in? If yes, `critical`. If no, `standard`.**

**Retired when:** a change every clause passed as `standard` is found by
review to have changed an existing caller's outcome, more than once over a
stated population — the test's coverage is then shorter than its claim — or
the changes it classes `critical` are shown, over a stated population, never
to have drawn a must-fix at independent review.

---

## The tiers

| Tier | Typical work | Review | Gates |
|---|---|---|---|
| `trivial` | Documentation, comments, data additions, ticket edits | None; author self-merges | Mandatory |
| `standard` | Most feature work — new validators, resolvers, queries, components | None; author self-merges after a complete PR description with evidence per criterion | Mandatory |
| `critical` | Anything the operative test catches | One approval from **another agent**, human or AI, who must verify the evidence and run the suite themselves | Mandatory |

Gates are mandatory at every tier. There is no tier that skips the four
machine checks — the tier governs *human and peer* review, not automated
review. The fifth gate, falsification, is discharged by the executor at every
tier, per `docs/quality-gates.md`, and independently verified only where the
tier summons a reviewer; at `trivial` and `standard` its recorded count stands
on the executor's word, which is a gap the tier table accepts and this
sentence names.

`trivial` work may share one batch ticket rather than take a ticket each;
the rule is in `docs/ticket-lifecycle.md`, "Batching trivial work".

**Retired when:** `standard`-tier work spot-checked by a reviewer draws must-
fix findings at a rate comparable to `critical`-tier review yield, over a
stated population; the tier that skips review then skips something.

---

## The scrutiny list, and why it is not a trigger

A handful of modules are where the operative test most often returns
`critical`: the central state object, the phase machine, the modifier
pipeline, the seeded random source, and the public action shapes.

Touching one of those is **a cue to run the test, not an automatic
escalation**. A purely additive extension that follows an established pattern
and changes no existing caller — a new optional field defaulting to null, a new
hook joining existing ones at a boundary, a new type nothing reads yet — stays
`standard`.

This distinction matters more than it looks. A model that escalates on file
paths trains contributors to treat escalation as noise, and an escalation
everyone ignores is worse than none.

**Retired when:** changes to the listed modules that the test classed
`standard` are found by review to have altered existing behaviour, more than
once over a stated population; the test's clauses are then not catching what a
path trigger would, and the argument against the trigger is weaker than its
cost.

---

## Separation of duties

The tier can move, but not freely, and not by the same party in both
directions:

- **The author proposes** the tier when writing the ticket.
- **The executor may raise** it — discovering mid-implementation that a change
  touches an existing contract — and records a one-line reason.
- **The executor may never lower it.**
- **Only the reviewer may lower** a tier the executor raised, and only as far
  as the operative test warrants, recording the reasoning.

The asymmetry is deliberate. A `critical` tier is what summons a second
reviewer, so an executor able to lower its own tier could dismiss its own
oversight. Raising is self-imposed cost and needs no check; lowering removes a
control and therefore cannot be done by the party the control is on.

This is the oldest idea in the document and the one that transfers furthest:
the party subject to a control does not get to remove it.

**Retired when:** the project has no reviewer distinct from the executor and
cannot obtain one, so the asymmetry has no second party to rest on. In this
repository ADR-0002 is the current answer to that, and the rule retires here
only if that answer is withdrawn.

---

## Why "another agent, human or AI"

Critical review requires a second reviewer that is not the executor. It does
not require a human.

An independent agent, given the ticket, the diff, the evidence and the two
questions in the next section, but not the executor's reasoning, catches a
specific and common failure: an implementation that
satisfies the letter of every acceptance criterion while missing their intent.
The reviewer has to verify the evidence and run the suite itself rather than
accept the executor's summary — which is the whole value, since a persuasive
summary of wrong work is the characteristic AI failure mode.

The reviewer works in a worktree of its own and never writes to the tree
under review; the rule and the check the executor runs afterwards are in
`docs/quality-gates.md`, "Review isolation".

What it does not substitute for is accountability. The independence is real;
the judgement is still mine.

**Retired when:** independent review of `critical`-tier work returns no must-
fix over a stated population of tickets. The current count against that is the
source wave's six of six and this repository's own record, which are in the
case study and the closed tickets.

---

## What a review reports

A critical-tier review answers two questions of the change, and records the
answers as two columns of findings in the pull-request description's Review
section:

1. **What does the change permit that the ticket says it must refuse?**
2. **What does the change refuse that honest work needs?**

**A finding in the second column is a must-fix of the same rank as a finding
in the first** — a must-fix being a finding the reviewer records as blocking
merge, as "When review ends" defines it; whether a finding blocks merge does
not depend on its column. Over-tightening is a defect, not a conservative
default. A reviewer briefed to look hard looks, unprompted, for one thing —
what the change lets through — and a review that runs for several rounds under
that brief tightens monotonically, because every finding adds a refusal and no
finding removes one. The scrutiny-list section above already says why that is
a defect: a control the controlled party ignores is not a control, and a
review that only ever tightens produces controls that get ignored.

The evidence is OMN-021 on the control-plane project that implements this
process mechanically. Its pull-request description's over-tightening
paragraph records four over-tightenings and names three with the round that
caught each: a rule that refused the board index every claim touches, making
every branch in the repository unmergeable, caught in round 4, one round
after it was written; a rule that denied on inherited duplicate identifiers,
stalling every branch in any corpus with a pre-existing collision, caught in
round 5; a rule that refused any non-Markdown file under the ticket
directory, with no achievable remedy, while two such files sat on the branch,
caught in round 6. Each was caught a round late, by the next reviewer,
incidentally, while looking for holes. A reviewer asked the second question
would have found the first in the round that introduced it, because the
answer was every branch, including the one under review.

**A tightening states its cost.** A first-column finding whose remedy adds
to a control — a list entry, a tier escalation, a refusal — states in the
same finding what the addition costs: which ordinary changes now pay the
control, measured where it can be measured. A finding that cannot say what
its remedy costs is incomplete. On OMN-021 a configuration filename was added
to the list that raises the review tier of any change touching it, matched
anywhere in the tree; the file it matched at the repository's own root is
touched by 5 of the 203 commits on that repository's default branch, counted
in OMN-021-001, item 6, and each of those now needs an independent approval. The
cost was measured after the fact, by the executor, for the maintainer. It
belonged in the finding. Commit counts against a default branch are one
measure, given as an example and not prescribed.

**Both columns on one rule in consecutive rounds is a class signal.** The
two columns have a failure mode of their own: round one finds, in the first
column, that a rule lets something through, and tightens it; round two
finds, in the second, that the tightening refuses honest work, and loosens
it; round three tightens it again. Each finding is correct on its own terms
and the loop never disagrees with itself. So: when a first-column finding on
a rule in one round is followed in the next round by a second-column finding
on the same rule that lies inside the previous round's fix, the round's
repair of that rule is a redesign against its class — the class obligation
in the contributor policy's §6, recorded in its form — and not a further
adjustment. The reviewer names the signal and records beside it the
adjustment it would otherwise have proposed, so that the falsifier below
can be read; the executor does the redesign, or repairs the instance and
says so in §6's words, which the next round then tests. Two findings on one
rule that are not inside each other's fix are two unrelated adjustments and
do not fire the signal, whatever columns they fall in; the distinction is
read from two fields the per-round record carries for every finding — the
column, and whether the finding sits inside the previous fix — and adds no
new judgement. Where the second-column finding matches the rule's stated
falsifier, "Retiring a control" governs instead. This is the single-rule
complement of the repairs-of-repairs signal in "When review ends", which
fires on the proportion of a round: that one fires when ping-pong is most
of what the round found, this one when one rule is ping-ponging inside a
round that is otherwise finding new things. What it refuses is a further
adjustment that would have been right; the cost of a wrong redesign is a
round. Its cost in the record is two fields on every finding — the rule
the finding landed on, and whether it sits inside the previous fix — and
findings exceed must-fixes: the round-1 review of c0111ae, the commit that
raised the rule's parent, returned 22 findings and 1 must-fix, per the
record in 3da6c57 that the ticket raising this rule quotes. The next round
reads the previous round's finding lines from the brief it is given or
from the ticket, where the executor may commit them with the repair.

**Retired when:** three rules sent to redesign by this signal each produced
a redesign whose effect the per-round record shows to be the same as the
adjustment the reviewer recorded beside the signal — the signal costing a
round and buying nothing, three times.

The reviewer receives the two questions as part of the brief, alongside the
ticket, the diff and the evidence. They are two columns and not a severity
scale because a scale asks the reviewer to rank a hole against an
over-tightening, which reintroduces the judgement the two questions exist to
separate. The reviewer answers both; what to do about the answers is the
executor's and the maintainer's.

**Retired when:** second-column findings over a stated population of critical-
tier reviews are all notes and never must-fixes, or every tightening finding's
cost line reads "cannot be measured"; the second question then finds nothing
that blocks, and the cost rule produces no measurement.

---

## When review ends

A review usually ends when a round returns clean. Where a round cannot return
clean, a rule is needed, because without one "every round found something"
reads as the review earning its keep — and under this model's own reasoning
it is the opposite. A process with no statement of what a converged review
looks like cannot be shown to have converged, only to have been stopped. The
falsification gate asks a test to name what would make it fail; the same is
asked here of the review.

One class of change guarantees a round that cannot return clean: an
enumeration maintained against an adversary — a list of paths, names or
shapes that a control must catch. A reviewer briefed to find the entry the
list is missing will find one every round, because the list is finite and the
adversary's options are not.

A round is one reviewer's pass over one commit, and the repair it produces. A
must-fix is a finding the reviewer records as blocking merge. A round ends the
loop **without a further fix** under any of three conditions. Each names where
its findings go.

1. **The round finds no must-fix.** Review is complete.
2. **Every must-fix in the round lies inside a limit the ticket already
   records** — an out-of-scope item, a stated narrowing, a child ticket. The
   reviewer's record says which limit each finding sits inside; the executor
   routes the finding but does not reclassify it, since the party subject to
   a control does not get to remove it. The findings go to the ticket that
   owns the limit, raised if it does not exist. Review of this ticket is
   complete, with the limit and the findings routed to it stated in the
   pull-request description as they are, not softened.
3. **Every must-fix in the round adds an entry to an enumeration the change
   maintains against an adversary.** The entries are added once; the list is
   recorded as best-effort with the review's coverage stated; and further
   rounds against the list are list-building, not review. A finding that
   adds an entry to a list is evidence the list is a list, not evidence the
   rules it serves are wrong, and it does not reopen review of those rules.

**The cap.** A ticket takes at most **three** review rounds before it blocks
to the maintainer with its review record attached. Three is a default, named
as one, and the reasoning is one ticket's record: on OMN-021, the control-
plane ticket this section was measured on, the per-round must-fix counts in
its Review section run 7, 5, 2, 3, 4, 2, 2, 2, 6, 5, 3, 1, 2, 2 over fourteen
rounds, the eight rules it built were unchanged after round 6, and every
finding from round 7 onward was in two path lists. Rounds 1 to 3 found the
rules' original defects; rounds 4 to 6 repaired the repairs, which is the
signal below; everything from round 7 was lists. Three is set one round past
the point where original rule defects stopped, and the record supports no
stronger claim for it than that. Blocking at the cap is a success path in
exactly the sense of the contributor policy's §3: the executor has correctly
identified that the loop is not converging, and the alternative is another
round that looks like progress. The record travels with the block: the per-
round table is appended to the ticket file under the `BLOCKER:` comment, since
the pull-request description it would otherwise live in is not written until
close.

The cap is not the rule; the conditions are. A cap alone ends a review that
is still finding rule defects, which is the wrong review to end. The
conditions end the review that cannot converge, and the cap catches the case
where nobody applied them.

**Repairs of repairs.** When a round's must-fixes are mostly inside the
previous round's fix, the next step is not another per-finding repair but a
redesign of the fix against its class — the class obligation in the
contributor policy's §6, referenced here and not restated. On OMN-021, 29 of
the 46 must-fixes, derived from the per-round figures in its Review section,
were defects in a fix rather than in the original work.

**The record.** The pull-request description's Review section carries, per
round: the round number, the must-fix count, where the findings sat (rules,
lists, documents, tests), how many sat inside the previous round's fix, and
the commit that repaired it. **The total is derived from the rows and never
asserted beside them.** OMN-021's own total drifted three times — its Review
section records "sixteen", "thirty-five" and "twenty-nine" — while it was
asserted rather than derived.

**Retired when:** a ticket blocked at the cap whose maintainer, reading the
record, orders a further round that finds a rule defect — the cap's own
falsifier, stated in the ticket that landed it — or the per-round record is
shown, over a stated population, never to have been read by anyone deciding
what to do next.

---

## Retiring a control

EM-006 demands of every test that it name the wrong implementation it rules
out, and "When review ends" demands of every review that it say what a
converged review looks like. This section makes the demand of a rule. A rule
that cannot say what evidence would retire it is an unpinned rule, in exactly
the sense that a test with a zero red count is an unpinned test: it is
there, it is passed, and it constrains nothing that can be checked. A control
set that can only grow is over-tightening by construction, whatever its
review brief says.

**Every rule states its falsifier.** Each rule in the documents under
`docs/` carries a line introduced by **Retired when:**, naming the evidence
that would show the rule refuses honest work or no longer catches what it
was added to catch — stated so that a reviewer could recognise it: a
measured cost, a class of change it blocks that the project needs, a failure
mode it was added for that a later control now covers. A rule whose
falsifier cannot be stated says so, in the words **no falsifier stated**, in
the same place. That is permitted, for the reason "repair of the instance"
is permitted under the falsification gate: it is a claim a reviewer can see
and hold the author to, where silence is not. A rule that says "no falsifier
stated" is the rule most worth a second look.

A falsifier may be a cost rather than a failure, and most are. "Do not
force-push to the main branch" has no observed failure that retires it; its
falsifier is on the cost side — retired when the project's history model
changes such that the rule protects nothing. A cost-side falsifier is not a
weaker form.

A rule stated in two documents carries one falsifier, stated where the rule
is stated in full and referenced from the other. The hooks rule — hooks may
not be skipped — is stated in the contributor policy's forbidden actions and
again in the quality gates; its falsifier lives with the policy.

**Where a second-column finding goes.** "What a review reports" gives a
review the means to find that a rule refuses honest work. This is where the
finding goes.

- A second-column finding that matches the stated falsifier of a rule
  **already in `docs/` at the change's baseline** is handled by extending the
  second condition of "When review ends" from the round to the finding: the
  finding lies inside a limit the rule itself recorded, so it goes to a ticket
  that owns it, raised if it does not exist, and that one must-fix is
  discharged by raising it. That ticket is a **retirement ticket**, critical
  tier under the process-surface clause of the operative test. It produces a
  decision record, per the decision-record process, carrying the rule's text
  as it stood and the finding that matched, and the rule leaves the document.
  Retired rules are kept in the record for the reason superseded decision
  records are kept: what was tried and why it stopped is most of the value.
- A second-column finding that matches the falsifier of a rule **the change
  under review itself adds** is a must-fix on the change, repaired in the
  round like any other. The defective rule does not ship and then get
  retired; it does not ship.
- **Amendment with record.** Where the match is technical and the correction
  small — a word, a scope, a threshold — the retirement ticket may amend the
  rule in place instead of removing it, provided the decision record carries
  the old text, the matching finding, and the new text. The record is the
  control; the removal is not. A ticket choosing amendment says in its
  pull-request description why the match was technical. Retirement is the
  default because an amended rule keeps its place and its authority with
  readers, and the amendment is invisible to anyone who did not read the
  diff; a retired rule leaves a gap a reader can see and a record a reader
  can find.
- A second-column finding that does **not** match the stated falsifier is a
  finding against the falsifier as much as against the rule. Either the rule
  is refusing something its author did not foresee, in which case the
  falsifier was too narrow and is widened by the retirement ticket the
  finding raises, as an amendment with record — one whose record carries
  the old and new falsifier text and the finding, and says why the finding
  was not foreseen rather than why a match was technical — or the finding
  is wrong. The
  review says which it found; what follows is the executor's and the
  maintainer's, as "What a review reports" says.
- A retirement ticket is not worked by the executor whose work the rule
  refused. The party subject to a control does not get to remove it, and
  raising the ticket is as far as that party goes.

**Who this binds.** A ticket that adds a rule states the rule's falsifier in
its Behaviour section, and a ticket that does not is not ready, in the sense
the ticket template uses that word. The obligation applies to tickets raised
after the ticket that landed this section closed; rule-adding tickets that
were already in `ready/` then are exempt, and each states the falsifier for
the rule it adds when it is worked, saying so in its pull-request
description. The exempt tickets are named in the decision record that landed
this section, not here.

**Retired when:** twenty rules carry stated falsifiers, ten second-column
findings have been recorded against rules that carry one, and none has
matched. That would show the falsifiers are decorative — written to satisfy
this section, not to be recognised — and a decorative falsifier is the defect
this section exists to remove. The first count is read from the Retired-when
lines in `docs/`, and is already past twenty at landing, so the condition is
the second. That is read from the Review sections of closed critical-tier
tickets, which record each finding's column; the rule a finding landed on is
readable once the per-round record carries it, which EM-014-001 adds, and
until then by re-reading the findings.
