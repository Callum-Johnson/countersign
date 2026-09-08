# ADR-0004: A change to a process document is critical when a rule or a procedure moves

- **Status:** proposed
- **Date:** 2026-09-07
- **Deciders:** maintainer, on the question EM-007-002 reserved
- **Related:** EM-007-002 (this decision, and the edge decided with it);
  EM-018-001 and EM-007-001, the worked examples on the `trivial` side;
  ADR-0002, whose Context sentence
  this narrows in reach; ADR-0001 (adopting the tier model here);
  `docs/tier-review-model.md`, "The operative test" and "Separation of
  duties"; `docs/adr-process.md`, "When to write one"

## Context

Two published statements gave different answers for the same change. The
operative test in `docs/tier-review-model.md` classes as `trivial` a change
where "nothing a program executes and nothing a caller reads as a contract
is touched", and names documentation in the `trivial` row of its tier
table. ADR-0002's Context says "Changes to process documents are
process-surface changes, which the operative test classifies as critical.
So this is not a rare case: on a repository whose content *is* process
documentation, most substantive work is critical tier." A one-word fix to
`docs/ticket-lifecycle.md` was therefore `trivial` by the model and
`critical` by the record.

The conflict was found twice by independent review — of EM-007 (finding 12
of round 2) and of EM-012-001 (finding R2.2 of round 2) — and four tickets
had already been closed on a narrow reading that appeared in no document:
EM-007-001, EM-010-002, EM-012-001-001 and the entries of the batch EM-017,
each recording the reading in its own Notes.

EM-007-002 raised the question and blocked on it under the contributor
policy's §3. Both readings were coherent, so this was not ambiguity; the
question was reserved because it resolves a conflict between a decision
record and the model that record governs, and because one of its answers
removes a control from the party the control is on. Three answers were set
out with their costs, and the maintainer answered on 2026-09-07.

One edge of that answer was not settled by it, and the independent review of
this change reached it in round 1 as finding R1.4: does the line reach a
change that corrects a restatement of a rule or a procedure, in a document
that is not where the question is settled, to agree with the document that
settles it, which is itself unchanged? `templates/TICKET.md`, "How to use
this template", is a procedure by the line above, and EM-018-001 rewrote two
of its steps to agree with `docs/ticket-lifecycle.md`, which it did not
touch, and closed `standard` with no independent review. EM-007-001, one of
the four closures the first answer preserves, is one step from the same
shape. The edge went back under §3 for the same reason the first question
did — both available answers are the maintainer's, and the executor could
only lower a tier by answering it — and the maintainer answered on
2026-09-07. Both answers are recorded here, on the same date.

Writing that answer down took two attempts. Round 2 of the independent
review, on 2026-09-08, returned two must-fixes on the entry that carries it, one in each
column: it permitted the removal of text unique to the restatement, and it
refused every such correction on a project that keeps no map. Round 1's
finding on the same entry had been a first-column finding, so the class
signal in `docs/tier-review-model.md`, "What a review reports", fired, and
the entry was redesigned rather than adjusted a third time. The maintainer's
answer is unchanged by that; what changed is the test the entry states for
recognising the case the answer names.

Round 3, on 2026-09-08, returned one must-fix and four notes, and the ticket
blocked at the three-round cap in `docs/tier-review-model.md`, "When review
ends". The maintainer ordered a fourth round on 2026-09-08. That must-fix
landed not on the entry carrying the answer but on the paragraph saying which
party may add to which list: the sentence round 2 added for how a reviewer
performs a widening reached **any** entry of the negative list, so an executor
whose own work a standing entry refused could have widened it inside the
round — the act "Retiring a control" reserves to a retirement ticket that
executor does not work. Round 4 bounds the route to an entry the change under
review itself adds. Neither of the maintainer's answers is touched by it.

## Decision

A change to a process document is `critical` when it adds, alters or
retires a rule or a procedure, and `trivial` when it does not.
`docs/tier-review-model.md`, "The operative test", states that line in
full — what a rule is, what a procedure is, what the words reach and what
they do not, which party may add to each of those two lists, and the
evidence that would retire the line — and is the authority on it.

ADR-0002's Context sentence keeps its conclusion for every change that
adds, alters or retires a rule or a procedure. What narrows is its reach:
it does not carry process-document changes that do neither. ADR-0002's
Decision — what critical-tier review requires, who may perform it, and what
that reviewer receives — is untouched, and the record keeps `status:
accepted`. It carries a dated annotation pointing here.

The four tickets closed on the narrow reading before it was written down
stand and are not reclassified. Correcting them was a consequence of the
answer that was not chosen.

**The edge, decided 2026-09-07:** the line does not reach a change that
corrects a restatement of a rule or a procedure, in a document that is not
where the question is settled, to agree with the document that settles it,
where that document is itself unchanged. Such a change is `trivial`. No rule
and no procedure moved, because the document that settles the question is
unchanged and what a contributor is bound to do is unchanged.

The second entry of the negative list in `docs/tier-review-model.md`, "The
operative test", carries that answer, and states the test it turns on:
**containment**, read from the change and from the documents as they stand.
A corrected restatement is `trivial` when nothing left the documents and
nothing entered them — every question the rewritten sentences answered
before the change is still answered in full by a document the change does
not touch, and the sentences now say nothing that document did not already
say. *In full* is text containment: the untouched document says everything
the removed text said, and not merely that it covers the same subject.
Deference and the contributor policy's map are how the untouched document
is found; they are evidence, and neither is required. EM-018-001 and
EM-007-001 are the worked examples on that side of the line, and both pass
containment in both directions. EM-018-001's `standard` closure stands and
is not corrected: `standard` is above what the line returns, and an executor
may raise.
EM-007-001 keeps its `trivial` closure.

## Rationale

Three reasons were recorded with the answer to the reserved question.

It matches what four closed tickets already did. The reading was the
repository's practice; the defect was that it lived in four ticket Notes
and in no document a contributor reads before a first edit.

It keeps the batching path usable here. `docs/ticket-lifecycle.md`,
"Batching trivial work", exists so that small changes do not each take a
ticket. Reading ADR-0002's Context as written would have removed that path
on this repository, because nothing here would ever be `trivial`.

The acknowledged cost is accepted rather than denied. The line between
"alters a rule" and "does not" is drawn by the executor, at the moment the
executor would prefer the answer to be `trivial` — ADR-0001's Alternative 3
in a different form. Two things hold it: "Separation of duties", under
which an executor may raise a tier and may never lower one, and the fact
that the line is now in a document, so a `trivial` claim on a
process-document change is checkable by anyone reading the closed ticket.

**The edge.** One reason was recorded with the second answer: no rule and no
procedure moved. What binds a contributor is the document where the question
is settled; a restatement elsewhere is a copy of that rule or that
procedure, and correcting the copy against an unchanged original leaves what
a contributor is bound to do exactly where it was.

**Why the entry tests containment rather than authority.** The first two
attempts at writing that reason down both asked which document had the
authority, and independent review found a defect in each: round 1's entry
was too narrow, reaching only a duplicated list, and round 2 found the
widened entry defective in both directions at once. It permitted the
removal of text unique to the restatement, because a paragraph called a
restatement could be deleted whole; and it refused ordinary work on any
adopting project that keeps no map, because where nothing defers no
document settles the question and every such correction returned
`critical`. Both defects have one source: the entry decided a tier from a
relationship between two documents, and that relationship is not a fact the
change carries. It had to be inferred, and where the inference failed the
entry either lowered too far or raised everything.

The maintainer's reason does not need the relationship. "What a contributor
is bound to do is as it was" is a claim about the documents before and
after, and it is answerable from the change: does every question the
rewritten sentences answered still have a document, untouched by this
change, that states it in full, and does the correction carry anything that
document did not already say. Containment answers both, from the diff and a
read of one other document. Deference and the map survive as the fastest
way to find that document, which is what they were always doing.

Its cost was stated with the answer and accepted rather than denied, and it
is larger than the first decision's. The negative list's second entry
reaches any restatement and not only a duplicated list, and the containment
read is made by the executor who would prefer `trivial` — ADR-0001's
Alternative 3 reached by a second route. What containment adds against that
is that the read is checkable: two documents at one commit, which a later
reader can repeat, where "which document was the authority" was an argument
nobody could settle. One rule and not a mechanism holds the rest:
"Separation of duties", under which an executor may raise a tier and may
never lower one. The falsifier below the line names the containment failure
in its own terms, on the occasion that supplies it, and names separately
the contributor-behaviour failure that occasion cannot supply.

## Consequences

- **Positive:** the question has one answer, in the document that settles
  which tier a change is, rather than two answers in two documents and a
  third in four ticket Notes.
- **Positive:** ordinary work on this repository — a corrected filename, a
  typo, a dead link — self-merges or batches, as it has been doing.
- **Positive:** the answer carries a falsifier with a stated occasion for
  its check, so the line can be shown wrong rather than argued about.
- **Negative:** the executor draws the line, on its own work, at the point
  where it benefits from the answer. The mitigation is a rule about who may
  move a tier, not a mechanism.
- **Negative:** changes that alter a rule or a procedure on a repository
  made of process documents summon an independent reviewer, and reviews of
  process documents run long. The round cap in `docs/tier-review-model.md`,
  "When review ends", applies.
- **Negative:** the edge decided on 2026-09-07 widens the exemption. A
  contributor may now correct any restatement of a rule or a procedure at
  `trivial`, where before the entry reached only a duplicated list replaced
  by a reference to it. A contributor who reads the restatement and not the
  document that states the rule in full does something different after such
  a change, and pays for it with no review; that is the second case the
  falsifier names, counted where it surfaces rather than on the reviewer's
  occasion, because no reading of closed changes produces it.
- **Positive:** the containment test costs a read of one other document and
  returns the same answer on a project that keeps no map as on this one. It
  also refuses what the relationship test permitted: text unique to the
  edited document cannot be removed at `trivial` by calling the paragraph
  around it a restatement, because the question that text answered is then
  answered in full nowhere.
- **Negative:** a change closed `trivial` under this line now marks itself
  in its pull-request description, so that the falsifier's population can be
  listed. That is a sentence per closure, and a closure that omits it is
  outside the population the reviewer reads. The sentence is written by the
  party the line is on, so the falsifier counts a closure found to have taken
  the line without it, whatever that closure turns out to have altered.
- **Negative:** where two documents state one question in full and disagree,
  correcting either against the other passes containment — the question stays
  answered in full — while a reader who had been following the corrected
  document is bound differently afterwards. The reason the entry rests on
  holds for the documents and not for that reader; the entry says so, and the
  falsifier's second limb is what counts the case.
- **Positive:** a review's second-column must-fix widens a negative-list entry
  inside the round only where the change under review adds that entry, which
  is the case in which nothing is yet in force to remove. A finding against an
  entry standing at the baseline goes to the retirement ticket "Retiring a
  control" routes it to, and that section keeps the ticket away from the
  executor whose work the entry refused.
- **Neutral:** `docs/adr-process.md`, "Decisions about the process are
  themselves ADRs", still says changing the process is a process-surface
  change the operative test classes as `critical`, which now reads wider
  than the model. Reconciling it is EM-007-002-002.
- **Neutral:** EM-018-001's `standard` closure stands under the edge
  decision and is not corrected, and EM-007-001 keeps its `trivial`
  closure. Both are named in "The operative test" as the worked examples on
  that side of the line.

## Alternatives considered

### Alternative 1: ADR-0002's Context governs as written

Every change to a process document is `critical` and summons an
independent reviewer. Rejected on cost: a typo fix in the lifecycle would
cost a review round; the batching path would become unusable here, since
nothing in this repository would ever be `trivial`; and the four tickets
closed on the narrow reading would have been closed at the wrong tier, so
the record would have to say so.

### Alternative 2: Amend ADR-0002 under the amendment-with-record path

Rewrite the Context sentence in place, with a record carrying the old text
and the new, per `docs/tier-review-model.md`, "Retiring a control".
Rejected because that path governs a second-column review finding matching
a rule's stated falsifier, and this was a maintainer's answer to a reserved
question, not a finding. No rule text leaves any document here, and the
sentence amended would be a Context sentence describing a consequence
rather than a rule with a falsifier of its own.

### Alternative 3: Leave the reading in ticket Notes

The status quo: four closed tickets state the narrow reading, and each new
ticket restates it. Rejected because a reading that lives in closed tickets
is not readable by a contributor before a first edit, cannot be held
against a `trivial` claim, and carries no falsifier — which is what let the
conflict survive two independent reviews.

The edge decided on 2026-09-07 had two alternatives of its own, and
the round-2 review of the entry that carries it recorded a third.

### Alternative 4: the line reaches a corrected restatement

A contributor reading the restatement performs the steps it states, so
rewriting them changes what a contributor does, whatever another document
says. Rejected because the document that settles the question did not move
and nothing a contributor is bound to do changed. Its cost, had it been
taken: EM-018-001 would be a closure at a tier this record contradicts, and
whether the closure is corrected or stands from 2026-09-07 forward would be
a further question of the same kind; and EM-007-001, one of the four
closures the first decision preserves, sits one step from the same shape.

### Alternative 5: a third negative entry, drawn to keep EM-007-001 and lose EM-018-001

An entry narrow enough to hold a duplicated list replaced by a reference,
and not a step rewritten to agree with the lifecycle. Rejected because no
principle separates the two: both correct a copy against an unchanged
original, and a line drawn between them would be drawn by where two closed
tickets happened to land rather than by what moved. A rule that can only be
stated as a list of the cases already met is the reading this record
rejected in Alternative 3.

### Alternative 6: keep the relationship test and adjust it again

Let deference answer where no map exists anywhere, and where nothing defers
let the executor record which document it treated as settling and take
`trivial`. This is the adjustment the independent review of round 2
recorded beside the class signal it named, and deliberately did not
propose, per `docs/tier-review-model.md`, "What a review reports". Refused
because it is a third adjustment to the same clause on the same question,
and the signal that fired says the repair is a redesign against the class
rather than a further adjustment. It also leaves the first-column defect
standing: a recorded judgement about which document was settling still
permits the removal of text unique to the restatement, since which document
was the authority says nothing about what left the documents. The class
signal's own falsifier — recorded with it in "What a review reports" —
counts redesigns whose effect turns out to be the same as the adjustment
refused; this redesign is one of the cases that falsifier will read, and it
differs from this alternative in that it refuses the removal of unique text
and needs no recorded judgement at all.

## Migration

No rule text leaves any document. `docs/tier-review-model.md`, "The
operative test", gains the line and its falsifier; ADR-0002 gains a dated
annotation below a horizontal rule, with its text above the rule and its
status unchanged. The four closures stand and are not touched.

The edge decision widens the second entry of that section's negative list
from a duplicated list replaced by a reference to any restatement corrected
against a document, untouched by the same change, that states the rule or
the procedure in full; states containment in both directions as the test;
names EM-018-001 beside EM-007-001 as the worked examples on that side, with
the containment read for each; and adds the containment failure to the
line's falsifier on the occasion that supplies it, with the
contributor-behaviour failure counted separately where it surfaces. A change
closed `trivial` under the line marks itself in its pull-request
description, which is what makes the falsifier's population listable, and a
closure found to have taken the line without that sentence is counted by the
falsifier. The paragraph on who may add to which list bounds the in-round
widening a review's second-column must-fix authorises to an entry the change
under review itself adds. No closed ticket is reclassified and no other
document changes. This record carries
both answers rather than a second record carrying the edge: the second
answer settles an edge of the line this record states, from the same
reserved question, answered by the same party on the same date, and this
record is `proposed` and lands with the change, so nothing accepted is being
amended. Splitting them would put half of one decision in a file a reader of
the other would have to be told about.

Two follow-ups are raised rather than worked here: EM-007-002-001, that the
section's one-line summary carries clauses 1 to 4 and not clause 5, and
EM-007-002-002, that `docs/adr-process.md` still states the wider reading.
