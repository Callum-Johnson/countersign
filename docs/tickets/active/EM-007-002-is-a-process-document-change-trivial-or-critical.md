---
id: EM-007-002
title: A change to a process document is trivial by the operative test and critical by ADR-0002
status: in-progress
tier: critical
complexity: S
dependencies: []
claimed_by: claude-opus-5
claimed_at: 2026-09-07
---

# EM-007-002 — Is a change to a process document trivial or critical?

## Context

Raised by the independent review of EM-007 (round 2, finding 12) and again
by the review of EM-012-001 (round 2, finding R2.2). Two published
statements give different answers for the same change.

ADR-0002's Context: "Changes to process documents are process-surface
changes, which the operative test classifies as critical. So this is not a
rare case: on a repository whose content *is* process documentation, most
substantive work is critical tier."

`docs/tier-review-model.md`, "The operative test", as EM-012-001 leaves it:
a change is `trivial` where "nothing a program executes and nothing a
caller reads as a contract is touched", and the tier table's `trivial` row
names documentation and ticket edits. A process document is read by
contributors, not by programs.

So a one-word fix to `docs/ticket-lifecycle.md` is `critical` by the
decision record and `trivial` by the model. Four tickets closed here on the
narrow reading — that ADR-0002 governs changes altering a rule or a
procedure, and not other documentation edits — and each recorded that
reading in its own Notes: EM-007-001, EM-010-002, EM-012-001-001, and the
entries of the batch EM-017. The reading is nowhere in the model or the
record it interprets.

## Specification

This ticket carries a question the contributor policy's §3 reserves to the
maintainer. It is not ambiguous — both readings are coherent — and it is
not the executor's to answer, because it resolves a conflict between a
decision record and the model that record governs, and because one of the
two available answers removes a control from the party the control is on.

The answers available, with what each costs:

1. **ADR-0002 governs as written.** Every change to a process document is
   `critical` and summons an independent reviewer. Cost: a typo fix in the
   lifecycle costs a review round; the batching path EM-012 added becomes
   unusable on this repository, because nothing here would ever be
   `trivial`; the four tickets closed on the narrow reading were closed at
   the wrong tier, and the record should say so.
2. **The narrow reading governs, and is written down.** A change to a
   process document is `critical` when it adds, alters or retires a rule or
   a procedure, and `trivial` when it does not. Cost: the line between
   "alters a rule" and "does not" is drawn by the executor, at the moment
   the executor would like the answer to be `trivial` — which is the
   failure ADR-0001's Alternative 3 rejected in a different form. The
   mitigation is that the executor may never lower a tier, only raise it.
3. **Something else**, including amending ADR-0002 under the
   amendment-with-record path, which is itself `critical` work.

What the executor needs in order to proceed: the maintainer's choice among
those, or a different one. The implementer then writes it into
`docs/tier-review-model.md` where the operative test states the `trivial`
line, records the decision per `docs/adr-process.md` since it is a workflow
rule changing, and — under answer 1 — corrects the record of the four
tickets closed at `trivial`.

## Acceptance criteria

1. AC1: `docs/tier-review-model.md` states, in one or two sentences, when a
   change to a process document is `critical` and when it is `trivial`.
2. AC2: The statement and ADR-0002 agree, or ADR-0002 is amended with a
   record per "Retiring a control".
3. AC3: The rule carries a **Retired when:** line.
4. AC4: Every ticket already closed at a tier the decision contradicts is
   named in the pull-request description, with what the record does about
   it.
5. AC5: Critical tier per ADR-0002: an independent agent reviews this
   against the artifacts and records findings in two columns.

## Out of scope

- Any change to the operative test's five clauses.
- Any change to what each tier requires. This ticket decides which tier a
  class of change is, not what that tier costs.

## References

- ADR-0002, Context — the sentence one reading follows.
- `docs/tier-review-model.md`, "The operative test" and "The tiers".
- ADR-0001, Alternative 3 — "'substantive' is decided by the person who
  wants the exemption, and the exemption widens", which is the hazard in
  answer 2.
- EM-007-001, EM-010-002, EM-012-001-001, EM-017 — closed on the narrow
  reading.

## Notes

The question is small and its answer is load-bearing: it decides whether
this repository's own work is reviewable at the cost it has been paying, or
at several times that cost.

**BLOCKER (2026-09-06) — discharged 2026-09-07 by the decision below. The
text is left as the record of why the work stopped.** The executor cannot
proceed. The Specification
above states a question that §3 reserves to the maintainer: which of ADR-0002
and the operative test governs the tier of a process-document change. Both
readings are coherent, so this is not ambiguity, and the test §3 states is
who answers rather than whether the executor could. Answering it in the diff
— by writing either reading into the model and seeing whether anyone
objects — is the invention §3 forbids, and it would be the executor choosing
which tier its own future work carries.

To proceed the executor needs the maintainer's choice among the three
answers stated above, or a fourth. Answer 1 additionally requires a decision
about the four tickets already closed at `trivial` on the narrow reading:
whether the record is corrected, or the closures stand and the rule applies
from the decision forward.

**Maintainer's decision (2026-09-07): answer 2.** The narrow reading
governs, and is written down. A change to a process document is `critical`
when it adds, alters or retires a rule or a procedure, and `trivial` when it
does not.

The reasoning recorded with the decision, in three parts:

- It matches what four closed tickets already did. EM-007-001, EM-010-002,
  EM-012-001-001 and the entries of the batch EM-017 each recorded the
  narrow reading in their own Notes and closed at `trivial` on it.
- It keeps the batching path `docs/ticket-lifecycle.md`, "Batching trivial
  work", added usable on this repository. Answer 1 would have removed it,
  because under answer 1 nothing here would ever be `trivial`.
- The acknowledged cost stands and is accepted: the line between "alters a
  rule" and "does not" is drawn by the executor, at the moment the executor
  would like the answer to be `trivial`. The mitigation is the
  separation-of-duties rule — an executor may raise a tier and may never
  lower it — and the written line is what a reviewer holds a `trivial`
  claim against.

The four tickets closed on this reading therefore stand and need no
correction. Correcting them was a consequence of answer 1, which was not
chosen.

**BLOCKER (2026-09-07) — Discharged (2026-09-07) by the maintainer's answer
recorded beneath it. The blocker text is left as the record of why the work
stopped.** The independent review of 49b5c00 reached, in
finding R1.4, a second question the contributor policy's §3 reserves. It is
not ambiguity: both answers are coherent, and answering either one in the
diff would narrow the maintainer's sentence or extend the maintainer's
carve-out to a closure the maintainer did not have in front of them. Every
other repair round 1 asked for raises a tier, which is the executor's to do
and is done; this one could only lower one.

`templates/TICKET.md`, "How to use this template", is an ordered sequence a
contributor performs, which the line written into
`docs/tier-review-model.md` calls a procedure. EM-018-001 rewrote its step 5
(the branch to commit on) and its step 1 (how the next lineage id is found)
— 12 insertions and 7 deletions in that file, plus one line added to
`.gitignore`, read from `git show --numstat 5750d73` — and closed
`standard`, self-merged, with no independent review. Each of those changes
brought the template into agreement with `docs/ticket-lifecycle.md`, the
document that settles the procedure, and the lifecycle itself was not
touched.

The question: **does the line reach a change that corrects a restatement of
a rule or a procedure, in a document that is not where the question is
settled, to agree with the document that settles it, which is itself
unchanged?**

The answers available, with what each costs:

1. **It reaches, and such a change is `critical`.** A contributor reading
   the restatement performs the steps it states, so rewriting them changes
   what a contributor does, whatever another document says. Cost:
   EM-018-001 is then a closure at a tier the decision contradicts, and
   whether the record is corrected or the closure stands from 2026-09-07
   forward is the question answer 1 of the Specification also carried, now
   asked of a ticket the decision did not name. And EM-007-001 — one of the
   four closures the decision preserves — is one step from the same shape,
   having replaced a duplicated list with a reference to it; the second
   entry of the negative list in "The operative test" would need restating
   on ground narrow enough to keep EM-007-001 and lose EM-018-001, or it
   falls with it.
2. **It does not reach, and such a change is `trivial`.** No rule and no
   procedure moved: the document that settles the question is unchanged,
   and what a contributor is bound to do is unchanged. Cost: the negative
   list's second entry widens from a duplicated list to any restatement,
   and whether one's own document was "the authority" is then decided by
   the executor who would prefer `trivial` — ADR-0001's Alternative 3 in
   the form this ticket's own cost paragraph names.
3. **Something else**, including a third negative entry drawn narrowly
   enough to cover EM-007-001 and not EM-018-001, or a reading that reaches
   the change but leaves closures made before 2026-09-07 alone.

What the executor needs in order to proceed: the maintainer's choice among
those, or a different one, and — under answer 1 — whether EM-018-001's
closure is corrected or stands. The round-1 record and the repair are in the
Review section of the description below, which travels with this block.

**Maintainer's decision (2026-09-07): answer 2.** The line does not reach
such a change: correcting a restatement of a rule or a procedure, in a
document that is not where the question is settled, to agree with the
document that settles it, where that document is itself unchanged, is
`trivial`.

The reasoning recorded with the decision: no rule and no procedure moved.
The document that settles the question is unchanged, and what a contributor
is bound to do is unchanged.

The cost the decision accepts, in the terms the answer was offered in: the
negative list's second entry widens from a duplicated list to any
restatement, and whether one's own document was the authority is then judged
by the executor who would prefer `trivial`. The mitigation is the
separation-of-duties rule and nothing else — an executor may raise a tier
and may never lower one.

EM-018-001's `standard` closure therefore stands and needs no correction:
`standard` is above what the line returns, and raising is the executor's to
do. EM-007-001 keeps its `trivial` closure, as it did under the first
decision.

**BLOCKER (2026-09-08) — Discharged (2026-09-08) by the maintainer's order
recorded beneath it. The blocker text is left as the record of why the work
stopped.** The ticket has taken its three review rounds and
blocks at the cap that "When review ends" sets in `docs/tier-review-model.md`.
Round 3 recorded one must-fix, and it is not repaired here.

R3.1: the who-may-add paragraph of "The operative test", as the sentence added
at `d867af9` leaves it — "The reviewer performs the act by recording it…" —
reaches a second-column must-fix against **any** entry of the negative list,
not only an entry the change under review itself adds. So a future executor
whose own work an entry refused could widen that entry inside the round, where
"Retiring a control" routes such a finding to a retirement ticket as an
amendment with record, and closes with "A retirement ticket is not worked by
the executor whose work the rule refused". The remedy is to bound the route to
an entry the change under review itself adds, leaving a pre-existing entry to
the ticket and the round that the preceding sentence already names. **That
remedy is one bounding clause**, it adds no per-review duty, and its cost is
that a future second-column must-fix on a baseline entry pays a round — over a
population of 0 today, since the whole list lands in this change. It is
deliberately not applied: applying it would be a fourth round, which the cap
reserves to the maintainer. The cost is stated here so the remedy can be
weighed without reading the document.

**What the maintainer is asked to decide.** Order a fourth round, which would
take R3.1 and carry the four notes R3.2 to R3.5 with it; or dispose of the
ticket another way — route R3.1 to a child ticket and close on the record as
it stands, accept the record unchanged, or answer differently. The question is
the maintainer's because the cap makes it so, not because the finding is
unclear.

**The trend the decision turns on.** Must-fixes ran 6, 2, 1 across the three
rounds — nine in total, derived from the per-round table below and not asserted
beside it. Three of those nine sat inside a previous round's fix: both of round
2's, inside round 1's repair, and round 3's single one, inside round 2's. The
falling count, and the redesign that round 2's class signal produced, are the
argument for one more round; that a third of the must-fixes are repairs of
repairs, and that round 3's single one is again inside the previous fix, is the
argument against it.

**Evidence the cap's own falsifier asks for.** "When review ends" retires the
cap when a ticket blocked at it has its maintainer order a further round that
finds a rule defect. This week the maintainer ordered fourth rounds on three
sibling tickets, and two of those rounds found real defects. That is evidence
toward the falsifier, and it is recorded here so this decision is taken with it
in view rather than against a cap read as a formality.

**An observation about the class signal's wording, recorded as fact and not as
a proposal.** The signal in `docs/tier-review-model.md`, "What a review
reports", did **not** fire on R3.1, for two reasons the reviewer records: R3.1
lands on a different rule from R2.2, and its direction is second-column then
first-column, which the signal's words do not name — the signal is written for
a first-column finding followed in the next round by a second-column one. The
reviewer flags that as worth the maintainer's eye. Separately, and as a second
fact rather than as an argument: a sibling ticket on the control-plane project,
OMN-022-003, round 3, blocked 2026-09-07, recorded a different gap in the same
signal's wording — findings ping-ponging across three rounds anchored on round
1's fix, which the signal's "inside the previous round's fix" clause does not
reach. Two independent instances of the signal's wording being narrower than
the pattern it names therefore now exist, which is the bar "A rule needs a
second instance" sets before a rule may be written as a ticket's own subject:
a second instance in a second ticket or on a second project. The bar is met.
Whether a rule is written, and in what words, is the maintainer's to direct;
no wording is proposed here.

The per-round record travels with the block, as "When review ends" requires,
because the pull-request description it would otherwise live in is not written
until close. It repeats the table in the Review section below rather than
pointing at it, so a reader of the blocker needs nothing else:

| Round | Must-fix | Where (rules / lists / documents / tests) | Inside previous round's fix | Repaired by |
|---|---|---|---|---|
| 1 | 6 | The process-document rule in `docs/tier-review-model.md`, "The operative test": its definition sentence, its negative list and its falsifier; the decision-record reasoning in this description; `docs/adr-process.md`; the AC4 claim | — | 99e7ae7 |
| 2 | 2 | The second entry of the negative list in `docs/tier-review-model.md`, "The operative test" — both must-fixes on that one entry — and its **Retired when:** line, where the three notes sit | 2 of 2 | d867af9 |
| 3 | 1 | The same rule in `docs/tier-review-model.md`, "The operative test": the who-may-add paragraph, whose permits-direction route reaches any negative-list entry and not only one the change adds (must-fix); entry 2's two-documents carve-out, whose stated reason fails in the case it carves out; the phrase "states that question's rule or procedure in full", which reads two ways; the self-marking population of the **Retired when:** line; and this description's cost paragraph, which never states containment's read as a cost | 1 of 1 | — |

Derived from the rows: 6 + 2 + 1 = nine must-fixes over the three rounds, of
which 2 + 1 = three sat inside the previous round's fix. Round 3's `—` in the
last column is nothing repaired, which is the point of the block.

**Maintainer's order (2026-09-08): a fourth review round.** The table above
is as it stood at the block; the Review section below carries the repair the
ordered round produced. The first of the two dispositions the block set out.
Round 4 takes R3.1 — repaired at its class, since the sentence it lands on is
a separation-of-duties defect and the class obligation in the contributor
policy's §6 binds the repair — and carries the four notes R3.2 to R3.5 with
it. Nothing about the record changes: the three rounds stand as recorded, the
cap stands at three, and the round is ordered rather than taken.

The cap's own **Retired when:** line in `docs/tier-review-model.md`, "When
review ends", retires the cap when a ticket blocked at it has its maintainer
order a further round that finds a rule defect. This is such an order. Whether
it counts toward that falsifier turns on what round 4 returns, which is not
known here; it is recorded so a later reader of the falsifier finds the case
rather than reconstructing it.

## PR Description

### Ticket
EM-007-002 — A change to a process document is trivial by the operative test
and critical by ADR-0002

### Tier
`critical` — a rule enters `docs/tier-review-model.md`, a decision record is
annotated, and a decision record is written. Each of the three is `critical`
under the operative test's fifth clause, under ADR-0002, and under the very
line this ticket writes down. Independent review per ADR-0002 ran once, on
49b5c00, and returned six must-fixes and three notes; the findings, the
repair and the class are recorded in the Review section below. One of those
findings, R1.4, reached a question the repair could not answer without
narrowing the maintainer's own sentence, and the ticket blocked on it; the
`BLOCKER (2026-09-07)` note in Notes above states the question, and the
maintainer answered it on 2026-09-07. The repair that answer made possible
is 8cf72a3. Round 2 ran on that head and returned two must-fixes and three
notes, both must-fixes inside round 1's fix, with the class signal named on
one of them; the redesign that answers them is d867af9. Round 3 ran on
a82d795, returned one must-fix and four notes, and repaired nothing: the
ticket blocked at the three-round cap on 2026-09-08 with its review record
attached, which is what "When review ends" asks of a review that has not
converged. The maintainer ordered a fourth round the same day. The repair
that round produced is 53125cb, and round 4's review is pending on it.

### Summary
The question this ticket carried was reserved to the maintainer under the
contributor policy's §3 and was answered on 2026-09-07 with the second of
the three answers the Specification set out. `docs/tier-review-model.md`,
"The operative test", now carries the line: a change to a process document
is `critical` when it adds, alters or retires a rule or a procedure, and
`trivial` when it does not. The paragraph says what a process document is,
what a rule is and what a procedure is, what the words reach and what they
do not, which party may add to each of those two lists, and it carries its
own **Retired when:** with the occasion on which that falsifier is checked.
ADR-0002 gains a dated annotation in the form the repository already uses;
nothing above its horizontal rule changes and its status stays `accepted`.
ADR-0004 records the decision, created `proposed`.

**The edge, answered 2026-09-07.** Round 1's R1.4 found that the line's reach
at a corrected restatement was undecided, and that the answer either way was
the maintainer's. It was answered with the second of the three answers the
`BLOCKER (2026-09-07)` note set out: the line does not reach such a change,
and it is `trivial`. The second entry of the negative list widens from a
duplicated list replaced by a reference to any restatement of a rule or a
procedure corrected to agree with a document, untouched by the same change,
that states it in full. EM-018-001 joins EM-007-001 as the worked example on
that side, and its `standard` closure stands: `standard` is above what the
line returns, and an executor may raise. Its one line added to `.gitignore`
is outside the process-document question and is not what the closure turned
on.

The test the entry states for recognising that case was written twice and
found defective twice. What it states after round 2 is **containment**, and
the block below says why.

**The falsifier reaches the widened entry, and says so.** The entry lowers a
tier, so its falsifier matters more than the paragraph's others. Round 1's
R1.7 found the original falsifier near-decorative because no occasion obliged
anyone to check it; the repair attached it to every independent review of a
critical-tier process-document change. Round 2's R2.4 and R2.5 found two
things wrong with what was then hung on that occasion, and both are repaired
at d867af9. The **Including** clause now names a containment failure — a
question the rewritten sentences answered that no untouched document states
in full, or a sentence the correction added that the untouched document did
not carry — because that is what a reader with two documents and one commit
can supply, where the older wording named a contributor's later behaviour and
the occasion produced no evidence of it. That failure is not dropped: it is
stated separately, counted from a `BLOCKER:` or a review finding that records
a contributor having followed a restatement, with the falsifier saying
plainly that nobody is obliged to go looking for it. And the population is
now listable — a change closed `trivial` under this line marks itself in its
description, and the command greps that sentence — where before the command
listed every `trivial` closure in `docs/tickets/done/`, 7 files at 53125cb
read from `grep -l "^tier: trivial" docs/tickets/done/*.md | wc -l`, of which
none closed under this line. The marker sentence returns 0 files at 53125cb
from `grep -rl "closed trivial under the process-document line"
docs/tickets/done/ | wc -l`, which is the population the line's own words say
is empty at landing, now readable as empty rather than asserted. Round 3's
R3.4 found that the marker is written by the party the line is on, so the
falsifier now counts a closure found to have taken the line without the
sentence, whatever that closure turns out to have altered.

**Widening an entry is adding one.** The paragraph on who may add to which
list said an entry to the negative list is lowering and belongs to the
reviewer and the maintainer, and said nothing about widening an entry already
there — which is what this change does. Found by the whole-section read at
8cf72a3 and closed in the same commit: widening an entry the second list
carries is the same act by another route and belongs to the same party. This
change did not do it alone; the maintainer answered first.

**The class round 2 repaired, and the signal that required a redesign.**
Round 2 returned two must-fixes, R2.1 in the first column and R2.2 in the
second, both on the same negative-list entry and both inside round 1's fix.
Round 1's finding on that entry, R1.4, was a first-column finding. That is
the pattern `docs/tier-review-model.md`, "What a review reports", calls a
class signal: a first-column finding on a rule in one round followed in the
next by a second-column finding on the same rule inside the previous fix. The
reviewer named the signal and recorded beside it, without proposing it, the
adjustment it would otherwise have offered — let deference answer where no
map exists anywhere, and where nothing defers let the executor record which
document it treated as settling and take `trivial`. **That adjustment is
refused, and the repair is a redesign**, which is what the signal requires.
The refusal is written into the record as ADR-0004's Alternative 6 so that a
later reader meets it where the decision is, and the class signal's own
falsifier — redesigns whose effect turns out to be the adjustment refused,
three times — has a case to read.

The class, in the form the contributor policy's §6 asks for — the question
which, asked of the whole change, produces R2.1 and R2.2 together: *the entry
decided a tier from a relationship between two documents — which one settles
the question — and that relationship is not a fact the change carries.* It
had to be inferred, from a map this repository happens to keep or from
deference a restatement may not express, and where the inference failed the
entry answered wrongly in whichever direction the failure ran. R2.1 is the
lowering direction: with no containment guard, anything a contributor calls a
restatement may be deleted at `trivial`, and text unique to that document goes
with it. R2.2 is the raising direction: with no map and no deference, no
document settles the question, so every correction of a restatement returns
`critical` — the class of work the maintainer's answer exists to keep cheap.
One source, two faces.

**The redesign.** The entry now tests **containment**, read from the change
and from the documents as they stand rather than from the documents' standing
relationship. For each question the rewritten sentences answered: *nothing
left*, so after the change a document this change does not touch states that
question's rule or procedure in full; and *nothing entered*, so the sentences
now say nothing that document did not already say. Both halves, every
question, or the entry does not apply. That is the maintainer's own reason —
what a contributor is bound to do is as it was — asked of the diff instead of
asked of the documents' authority, and it is checkable by a later reader,
which "which document had the authority" never was.

*Siblings the class question enumerates, with what a reader does differently;
the change has no suite.*

1. **R2.1's face.** Text unique to the edited document, removed, now
   **retires a rule or a procedure** and is reached by the bold words,
   "whatever the paragraph around it is called". A reader who deletes a
   paragraph and calls it a restatement is told that naming a paragraph a
   restatement does not make what is unique to it a copy, and summons a
   reviewer. Raises.
2. **R2.2's face.** A reader on an adopting project with no map, correcting a
   restatement that cites nothing, reads the other document for the question
   and answers from containment. Where before the reader had no settling
   document and returned `critical`, the reader now self-merges or batches.
   Lowers, and is the widening R2.2 names.
3. **The partial restatement.** A reader correcting a partial restatement
   gets `trivial`; a reader extending one gets `critical`, because the
   correction then carries what the untouched document did not. The entry
   says so, and the difference is in the diff. Raises against the old entry,
   which said nothing about it.
4. **The direction reversal.** A reader who edits the document that states
   the rule in full so that it agrees with a partial restatement elsewhere
   gets `critical`, because no untouched document then states the question in
   full. The old entry answered this only through the authority judgement.
   Raises.
5. **Two documents, neither deferring.** Either is the untouched document for
   a correction of the other, and containment still answers. Where the entry
   at 8cf72a3 sent this to the bold words, a reader now self-merges it if
   nothing left and nothing entered. Lowers, and it is the same widening as
   sibling 2: containment makes the two cases one, because what told them
   apart — which document had the authority — was never readable off the
   documents.
6. **Deference and the map.** Kept, demoted from test to evidence: they are
   how a reader finds the document to check, and neither is required. A
   reader with a citation checks one document; a reader without reads for
   one. R2.3's note falls out here — "by naming it" is gone with the test it
   qualified, so a mere mention can no longer supply an authority. Raises
   against the old wording.

Siblings 2 and 5 lower, and lowering an entry the negative list carries is
the reviewer's and the maintainer's under the paragraph on who may add to
which list. Both are written because round 2's second-column must-fix names
them: the reviewer recorded that the entry refuses the class of work the
decision exists to keep cheap, and the executor wrote the widening that
finding names and no more. The paragraph did not say how a reviewer performs
that act, which the whole-section read caught and d867af9 fixed; without
that sentence a second-column must-fix on an entry this change adds would
force a block rather than a repair. Round 3 found that the sentence as
d867af9 left it reached every entry and not only those, and 53125cb bounds
it — see **The class round 3 repaired** below.

**The class round 3 repaired.** R3.1 lands on the sentence added at d867af9
for how a reviewer performs a widening, and it is a separation-of-duties
defect rather than a wording defect: as written the route reached a
second-column must-fix against **any** entry of the negative list, so a
future executor whose own work a standing entry refused could have widened
that entry inside the round. That is the act "Retiring a control" reserves
to a retirement ticket, which the same section says "is not worked by the
executor whose work the rule refused". The class the contributor policy's
§6 asks for — the question which, asked of the whole change, produces R3.1
and its siblings: *which routes does this change give an executor to change
a control that constrains it?*

The whole change was swept for such routes. Each is named below with whether
it is bounded correctly; the change has no suite, so each says what a reader
does differently. Two were not bounded, and both are repaired at 53125cb.

1. **Adding an entry to the *reaches* list.** Open to the executor and
   bounded correctly: an entry there raises, and raising is self-imposed
   cost under "Separation of duties". A reader that meets a case the bold
   words reach writes the entry alone.
2. **Adding an entry to the negative list.** Lowers, and closed to the
   executor: it belongs to the reviewer and the maintainer. A reader that
   wants one raises a ticket and pays a round. Bounded correctly.
3. **Widening an entry the negative list already carries.** Named as the
   same act by another route and left with the same party, at 8cf72a3, so
   the asymmetry cannot be walked around by editing an entry instead of
   writing one. Bounded correctly.
4. **The in-round widening a review's second-column must-fix authorises.**
   **Not bounded, and repaired.** The route now reaches only an entry the
   change under review itself adds, for the reason "Retiring a control"
   gives for a rule the change adds — the defective entry does not ship and
   then get widened; it does not ship. A reader holding a second-column
   must-fix against an entry that stood in the document at the change's
   baseline now writes no widening in the round: it goes to the ticket and
   the round the preceding sentence names, which is the retirement ticket
   "Retiring a control" routes such a finding to. Raises against the
   sentence as d867af9 left it. The trailing citation goes with it: it now
   cites the principle for a rule the change adds, where before it cited
   "Retiring a control" on a finding *matching* a falsifier, which is
   bullet 2's case and not this one.
5. **Who works that ticket.** The paragraph sent an executor to a ticket
   and a round and stopped there, so a reader could raise the ticket and
   then work it. **Not bounded, and repaired in the same sentence:** the
   ticket is the retirement ticket, and that section adds who works it —
   not the executor whose work the entry refused. A reader that raises one
   now reads, at the point of raising, that it is not its own to work.
   Raises.
6. **The marker sentence that puts a closure in the falsifier's
   population.** Written by the party the line is on, which is R3.4: a
   closure that took the line and omitted the sentence was outside the read
   that would catch it. **Not bounded, and repaired:** a closure found to
   have taken this line without the sentence counts toward the same "more
   than once", counted where it surfaces, whatever that closure altered. A
   reader that omits it does not thereby leave the population. Raises —
   toward retiring the line in favour of ADR-0002's Context read as
   written.
7. **The containment read.** Answered by the executor on its own work. Not
   a route to change a control but to apply one leniently, and it is the
   cost the maintainer accepted on 2026-09-07: held by the rule that an
   executor may raise and never lower, by these words sitting in a document
   rather than in ticket Notes, and by the falsifier that counts a misread.
   Bounded as far as a rule and not a mechanism can be; unchanged by this
   round, and stated as a cost in the document by R3.5's repair.
8. **The falsifier's occasion.** Discharged by the reviewer of a
   critical-tier process-document change, which is not the party the line is
   on. The residual — a change the executor closes `trivial` summons no
   reviewer of its own — is named in the falsifier and in "The tiers", and
   is not a route this change opens. Bounded correctly.
9. **The line's own falsifier.** The **Retired when:** line retires the line
   in favour of ADR-0002's Context read as written, which raises: an
   executor gains nothing by triggering it. Bounded correctly.
10. **The dated-annotation entry.** A reader could change how a decision
    record is read and call the change an annotation; round 1's R1.1
    narrowed the entry so that an annotation changing how a decision is read
    is `critical`. Bounded correctly, in round 1.

Routes 4, 5 and 6 all tighten, so all three were the executor's to write:
"Separation of duties" gives an executor the raising direction and denies it
the lowering one, which is the same asymmetry the round-1 class turned on.

**Whether a decision record is owed: yes.** Round 1 disagreed with the
answer this description gave at 49b5c00, and the disagreement holds when the
words of `docs/adr-process.md`, "When to write one", are read against this
change rather than against the four rule-adding tickets that came before it.

The negative limb reaches "a rule added inside a document, or extended in
place one rule at a time, **under an existing decision** — one that changes
what the process asks at one step … and **sits under the decision that put
that step there**". This change does not sit under ADR-0002. It narrows what
ADR-0002's Context sentence reaches, which the annotation on that record
says in those words: "What narrows is the sentence's reach". A rule that
constrains the decision above it is not a rule extended in place beneath it,
and the limb's second condition is unmet.

The positive limb reaches a decision that changes "how the process itself is
governed — the form every rule takes, **who may review or approve**, whether
the process applies to the repository at all". What was decided is whether a
class of this repository's work summons an independent reviewer at all. On a
repository whose content is process documentation, that class is most of the
work: ADR-0002's own Context says so. A decision that moves most of a
repository's work from a tier that summons a second reviewer to a tier that
does not is a decision about who reviews, in the plain sense of the limb.
The section's test reads the same way — the constraint is not an existing
decision's applied at one step, since the existing decision is the one being
narrowed.

The precedents cited at 49b5c00 do not carry the weight put on them.
EM-010-002 annotated ADR-0002 where two of its sentences had fallen *behind*
the model, and recorded the model as governing; EM-012-001 added a
distinction where the document had none. Neither narrowed a record. The
practice `docs/adr-process.md` names — EM-008, EM-009, EM-010, EM-011,
EM-012, EM-016, EM-019-001 — is rules added under decisions already
recorded, which is the shape this change is not.

`docs/adr/` therefore holds four records at 99e7ae7 against three at
60f39fb, read from `git ls-tree --name-only <commit> docs/adr/ | wc -l`.
ADR-0004 is created `proposed` and moves to `accepted` in the closing
commit, as ADR-0003's own status line and `templates/ADR.md` step 3
establish. The ticket's Specification said a record was owed "since it is a
workflow rule changing"; the line EM-019-001-001 drew since narrows that
trigger, and the reasoning above is why this change is on the trigger's side
of the narrowed line rather than beneath it.

**Whether the edge is owed a record of its own: no, and ADR-0004 says why.**
The second answer settles an edge of the line ADR-0004 states, comes from the
same reserved question, was given by the same party on the same date, and
ADR-0004 is `proposed` and lands with this change, so nothing accepted is
being amended by carrying it. Splitting the two would put half of one
decision in a file a reader of the other would have to be told about, which
is the failure `docs/adr-process.md`'s own Retired-when line names — records
nobody reads. `docs/adr/` therefore still holds four records at 53125cb
against three at 60f39fb, by the command above; the edge adds a section to
one rather than a fifth file.

**Second-instance bar.** This ticket was raised at fc9f592 and EM-021 closed
at 3578199, with fc9f592 an ancestor of 3578199 — read from `git merge-base
--is-ancestor fc9f592 3578199` — so the bar in `docs/tier-review-model.md`,
"A rule needs a second instance", does not bind it. Its Context names two
instances regardless: the independent review of EM-007 (finding 12 of round
2) and the independent review of EM-012-001 (finding R2.2 of round 2), each
finding the same conflict on this repository, both readable in
`docs/tickets/done/`. The bar also "does not reach a repair of the change
under review", which is what round 1's six must-fixes produced.

**The class this round repaired.** The class, in the form the contributor
policy's §6 asks for — the question which, asked of the whole change,
produces R1.1, R1.2 and R1.9 together: *which clause of what was written
makes the maintainer's sentence operable, and which one makes it narrower?*
The maintainer's answer was one sentence. Everything the paragraph adds
either helps a contributor answer that sentence without asking, which raises
or leaves the tier where the sentence puts it, or takes a change out of the
sentence, which lowers it. "Separation of duties" gives an executor the
first and denies it the second, and that asymmetry — not the reasonableness
of any particular clause — decides which the executor may write.

The siblings the question enumerates are every clause of the paragraph at
49b5c00. Each is marked and accounted for; with no suite, each says what a
reader does differently.

*Raising or neutral, kept as written:*

1. The bold sentence itself. Neutral — it is the maintainer's decision
   quoted. A reader gets the maintainer's answer rather than four ticket
   Notes.
2. **A rule**, with "widening or narrowing an existing rule alters it, and
   so does moving where a question is settled". Raises: a scope change and a
   relocation now count as alterations that a reader might have called
   editorial.
3. **A procedure**, with "changing what a step produces". Raises: a step
   rewritten without being added or removed now counts.
4. **A decision record**. Raises: writing one, or changing what one decides,
   is `critical` where a reader might have called it documentation.
5. "Neither list is closed … answered by asking whether a rule or a
   procedure moved." Raises: an unmatched change goes back to the bold
   words rather than out of them.
6. The two worked examples, EM-012-001 and EM-007-001. Neutral — both are
   closures the maintainer's decision already names.
7. The cost paragraph. Neutral — it states the hazard the maintainer
   accepted.
8. The **Retired when:** line. Neutral in direction: it retires the line in
   favour of the wider reading.

*Lowering, and accounted for:*

9. "A process document states rules a contributor follows — the class the
   contributor policy's map-keeping rule governs". **Removed.** That class
   is map-named documents plus `docs/`/`templates/`, so a root-level policy
   file on an adopting project fell in no category and came out `trivial`.
   The definition is now by function, and the map-named documents are added
   to the class rather than bounding it, so nothing leaves. A reader with a
   root-level `AGENTS.md` now gets `critical` for a rule change in it, and a
   reader of `DISCLOSURE.md`, which the map names and which states no rules,
   is not told it is outside the class. (R1.2, R1.3)
10. "A dated annotation … that leaves every rule and every decision as it
    stands." **Narrowed** to "leaves every rule as it stands and changes how
    no decision is read". The clause as written exempted an annotation that
    narrows a record, which is what this change's own annotation to ADR-0002
    does, and it contradicted the third *reaches* entry above it. A reader
    annotating a record to change how it is read now summons a reviewer.
    (R1.1)
11. "A reference the document states wrongly, corrected." **Narrowed** with
    a guard: the corrected reference must name what the document already
    pointed at. A reader who repoints a reference at a different place has
    moved where a question is settled, which the first *reaches* entry
    catches.
12. "A list duplicated from another document, replaced by a reference to the
    list it duplicated, where that list is unchanged." **Kept** in round 1,
    because the maintainer's decision requires it: EM-007-001 is exactly this
    shape and is one of the four closures the decision preserves. Removing it
    would contradict the answer given. **Widened after the maintainer's
    answer of 2026-09-07**, to any restatement of a rule or a procedure
    corrected to agree with an unchanged settling document. The widening
    lowers, so it was not the executor's to make: it was routed as entry 14
    below and made only once answered. **Redesigned at round 2** — the test
    the entry states for recognising that case is now containment, per **The
    class round 2 repaired** above; the maintainer's answer is untouched by
    that.
13. "Wording that leaves every rule's conditions and every procedure's steps
    as they were." **Kept** — it is the plain content of "does not alter a
    rule or a procedure", and it is what leaves ordinary work `trivial`.
14. How far entry 12 reaches: whether correcting a *restatement* of a rule
    or a procedure, in a document that is not where the question is settled,
    to agree with an unchanged document that is, alters a procedure.
    **Deferred to the maintainer** — the `BLOCKER (2026-09-07)` note above —
    because answering it either narrows the maintainer's sentence or extends
    a carve-out to a closure the maintainer did not have in front of them.
    **Answered on 2026-09-07: it does not reach, and such a change is
    `trivial`.** Written in as the widening of entry 12, with "the document
    that settles it" defined by function, EM-018-001 named beside EM-007-001
    as the worked example, and the case named in the falsifier. A reader
    correcting a restatement against an unchanged authority now self-merges
    or batches it, where round 1's text left the reader with no entry and
    sent the change back to the bold words. Round 2 found the "authority"
    half of that wording defective in both columns, and it is redesigned at
    d867af9; see **The class round 2 repaired** above.

Two clauses are added by these repairs and both are raising: the two lists
are marked for who may add to which, so that a future executor reads the
asymmetry at the point where it would otherwise widen the exemption; and,
after the whole-section read at 8cf72a3, widening an entry the negative list
already carries is marked as the same act as adding one, so the asymmetry
cannot be walked around by editing an entry instead of writing one.

**The reconciliation gap, and why it goes to a ticket.** R1.5 found
`docs/adr-process.md`, "Decisions about the process are themselves ADRs",
still saying "Changing the process is a process-surface change, which the
operative test classifies as `critical`" — now wider than the model, which
is the identical defect to ADR-0002's Context. It is real and it is not
repaired here. Repairing it means altering a rule in a third process
document, one no acceptance criterion of this ticket names, and by the line
this ticket writes that is `critical` work in its own right. Its own
**Retired when:** — "the tier model ceases to class the process surface as
`critical`" — is not matched, since the model has narrowed the surface
rather than ceased to class it, so "Retiring a control" does not route it
either. Widening a six-must-fix change, blocked at the time on a reserved
question, by a second document's rule
edit is a judgement worth stating rather than making quietly: it is routed
under §4 as **EM-007-002-002**, `ready`, proposed `critical`, and named in
ADR-0004's Consequences so that a reader of the record meets the gap rather
than discovering it. A reader who takes the wider sentence at face value in
the interval gets `critical` for a change the model calls `trivial`, which
raises and never lowers, and is the safe direction to be wrong in while the
ticket waits.

### Acceptance criteria
- [x] AC1: `docs/tier-review-model.md` states when a change to a process
  document is `critical` and when it is `trivial` — the paragraph beginning
  **A change to a process document** in "The operative test", at 53125cb.
  The line is one sentence: `critical` when the change adds, alters or
  retires a rule or a procedure, `trivial` when it does not. What surrounds
  it is what makes the sentence usable without asking — what a process
  document is, the two definitions, the two lists with the note that neither
  is closed and who may add to or widen which, and three closed tickets, one
  on the `critical` side and two on the `trivial` side. After the round the
  maintainer ordered on 2026-09-08, the who-may-add paragraph also says when
  a widening happens inside a round and when it takes a ticket: only an entry
  the change under review itself adds is widened in the round.
- [x] AC2: the statement and ADR-0002 agree, and the record is annotated
  rather than amended — see the annotation dated 2026-09-07 under
  EM-007-002 at the end of
  `docs/adr/0002-critical-tier-review-in-a-single-maintainer-repository.md`,
  the third annotation on that record, read from `grep -c "^## Annotation"
  docs/adr/0002-*.md` at 53125cb against two at 60f39fb. What agrees is the
  Decision, which is untouched and says nothing about which changes are
  `critical`. What was wider than the practice is one Context sentence, and
  the annotation records its narrowed reach, what stands, the reasoning, and
  ADR-0004. The amendment-with-record path of "Retiring a control" was not
  used: that path governs a second-column review finding matching a rule's
  stated falsifier, and this is a maintainer's answer to a reserved
  question, with no rule text leaving any document.
- [x] AC3: the rule carries a **Retired when:** line — the one immediately
  beneath the paragraph. It names the evidence (a change closed `trivial`
  under the line, found to have added, altered or retired a rule or a
  procedure after all, more than once), the population (the
  process-document changes closed `trivial` under the line, counted one per
  change and not one per ticket, since `docs/ticket-lifecycle.md`,
  "Batching trivial work", puts many in one file), and — new in this round —
  the occasion on which it is checked: every independent review of a
  critical-tier process-document change, with the command that lists the
  population. New with round 2, per R2.5: the population is a set a reader
  can list rather than a filter stated in words — a change closed `trivial`
  under this line marks itself in its description, and `grep -rl "closed
  trivial under the process-document line" docs/tickets/done/` returns 0
  files at 53125cb, against the 7 that `grep -l "^tier: trivial"
  docs/tickets/done/*.md` returns there, none of which closed under a line
  that lands with this ticket. New with the round the maintainer ordered on
  2026-09-08, per R3.4: the marker is written by the party the line is on, so
  a closure found to have taken the line without the sentence counts toward
  the same "more than once", whatever that closure turns out to have
  altered. New with the maintainer's answer of 2026-09-07
  and reworked at round 2, per R2.4: the falsifier names the widened entry's
  own failure as a containment misread, which the stated occasion supplies,
  and states the contributor-behaviour failure separately, counted from a
  `BLOCKER:` or a review finding, with the falsifier saying nobody is obliged
  to hunt for it.
- [x] AC4: The four closures the decision names — EM-007-001,
  EM-010-002, EM-012-001-001 and the entries of the batch EM-017 — stand,
  and the record does nothing to them; reclassifying them was a consequence
  of answer 1, which was not chosen. Each recorded the reading in its own
  Notes before it was written down, checked by reading all four at claim.
  Round 1 found a fifth ticket the criterion reaches and the maintainer's
  carve-out does not name: **EM-018-001** rewrote `templates/TICKET.md`'s "How to use
  this template" steps — 12 insertions and 7 deletions there, plus one line
  added to `.gitignore`, read from `git show --numstat 5750d73` — and closed
  `standard`, self-merged, with no independent review. Whether that is a
  closure at a tier the decision contradicts was the question of the
  `BLOCKER (2026-09-07)` note, and it was answered on 2026-09-07: it is not.
  The line does not reach a corrected restatement, so EM-018-001's change is
  `trivial` under it and closed one tier above that, which an executor may
  do. Its `standard` closure stands and the record corrects nothing; the
  ticket is named in "The operative test" as the worked example instead. No
  ticket closed before this change is at a tier this decision contradicts.
  Note also that the repair of R1.1 means the EM-010-002 shape
  — an annotation that changes how a decision is read — costs a round from
  here on; the closure itself stands, since the decision governs closures
  from 2026-09-07 forward.
- [ ] AC5: four rounds are recorded below in two columns, three run and the
  fourth pending. Round 1 returned six must-fixes and three
  notes, and the repair of its last open finding is 8cf72a3. Round 2 returned
  two must-fixes and three notes, both must-fixes on one negative-list entry
  and both inside round 1's fix, with the class signal named on R2.2; the
  redesign that answers them is d867af9, and the adjustment the reviewer
  recorded beside the signal is refused, in the Review section and in
  ADR-0004's Alternative 6. Round 3, on a82d795, returned one must-fix and
  four notes and repaired nothing: R3.1 lies inside no limit this ticket
  records, so no condition of "When review ends" ended the loop and the cap of
  three rounds did. The maintainer ordered a fourth round on 2026-09-08, and
  the repair it produced is 53125cb: R3.1 at the class **The class round 3
  repaired** states, with the ten routes that question enumerates, and the
  four notes taken with it. This criterion stays unticked because round 4's
  review is pending on 53125cb. The branch is left checked out.

### Falsification
N/A — a documentation change with no suite. Per acceptance criterion, what a
reader does differently:
- AC1 — a contributor whose change touches a document that states rules or
  procedures, wherever it sits, reads the paragraph and answers the tier
  question without asking anyone, where before the model returned `trivial`
  and ADR-0002 returned `critical` and nothing said which governed. A
  contributor correcting a wrong filename that still points where it pointed
  self-merges it or batches it; a contributor adding a rule, changing a
  threshold, moving where a question is settled, rewriting what a step
  produces, or annotating a record to change how it is read summons an
  independent reviewer. A contributor on an adopting project whose rules live
  in a root-level file gets the same answer as one whose rules live under
  `docs/`.
- AC2 — a reader of ADR-0002 who reaches the Context sentence now reaches
  the annotation with it, and does not conclude that a typo fix in
  `docs/ticket-lifecycle.md` needs an independent review. A reader auditing
  the four `trivial` closures against that sentence finds them answered
  rather than unexplained. A reader who wants the reasoning rather than the
  annotation's summary of it opens ADR-0004.
- AC3 — a reviewer of a critical-tier process-document change now has an
  occasion on which the falsifier is checked, a command that lists what to
  check, and a population counted in changes rather than tickets. Before the
  repair the line named a spot-check nobody was obliged to make, over a
  population that contained nothing closed under the line, so a reader could
  read the falsifier and do nothing. After the maintainer's answer, a
  reviewer on that occasion is also told, in the falsifier's own words, what
  the widened entry's failure looks like, so the entry that lowers furthest
  is the one the reviewer is least likely to pass over. After round 2 that
  failure is stated as a containment misread, which the occasion supplies,
  and the reviewer lists the population by grepping the sentence a closure
  writes about itself rather than reading every `trivial` closure in the
  directory — 0 files against 7 at 53125cb, by the two commands in the
  Summary. After the ordered fourth round a reviewer also counts a closure
  that took the line and left the sentence out, so a contributor cannot leave
  the population by omitting it. The contributor-behaviour failure is still
  counted, from a `BLOCKER:` or a review finding, and the falsifier now says
  nobody is obliged to hunt for it rather than implying a check it does not
  have.
- AC4 — a maintainer reading the record sees why four closures stand, sees
  what was asked about the fifth and what was answered, and sees that no
  closure is corrected. A contributor correcting a restatement against an
  unchanged authority self-merges or batches it and does not open a ticket to
  ask; and after round 2 a contributor who cannot say which document the
  others defer to reads for the document that states the question in full
  and answers from containment, on a project with a map or without one,
  where before that contributor got `critical` from the bold words. A
  contributor who deletes a paragraph unique to the document it sits in gets
  `critical`, whatever the paragraph is called.
- AC5 — a reviewer of round 4 reads round 1's nine finding lines, round 2's
  five and round 3's five, each with its column, the rule it landed on and
  whether it sits inside the previous round's fix; the three class statements
  beside them; the adjustment the round-2 reviewer recorded and the record of
  its refusal; and can test whether the redesign is a redesign or the refused
  adjustment under another name, and whether the route sweep of round 3's
  class missed a route.

Round 1's six must-fixes are repaired at the class stated above, in the
form the contributor policy's §6 asks for: the class question, the siblings
it enumerates, and what a reader does differently for each, since the change
has no suite. R1.4, R1.5 and R1.7 fall outside that class and are repaired
as instances, in those words — R1.4 by naming EM-018-001 and routing the
question the record could not answer to the maintainer, then writing the
answer in at 8cf72a3, R1.5 by routing to EM-007-002-002 with the
scope judgement stated, R1.7 by giving the falsifier an occasion.

Round 2's two must-fixes are repaired at the class **The class round 2
repaired** states, with the six siblings that question enumerates and what a
reader does differently for each. R2.3 falls out of the redesign and is not a
separate repair. R2.4 and R2.5 are on the falsifier rather than on the entry
and are repaired as instances, in those words — R2.4 by naming a failure the
stated occasion supplies and moving the contributor-behaviour failure to the
occasion that does supply it, R2.5 by making a closure mark itself so that
the population is a set a reader can list.

Round 3's single must-fix is repaired at the class **The class round 3
repaired** states — *which routes does this change give an executor to change
a control that constrains it?* — with the ten routes that question enumerates
and what a reader does differently for each, since the change has no suite.
Two of the ten were unbounded: R3.1's, and the one R3.4's note names, which
is a sibling of the class rather than a separate repair. R3.2, R3.3 and R3.5
fall outside the class and are taken as instances, in those words — R3.2 by
saying in the entry what it permits where two documents disagree and where
that case is counted, R3.3 by defining "in full" as text containment and
naming the rewritten sentences pre-state in one half of the test and
post-state in the other, R3.5 by stating the containment read as a cost in
the cost paragraph where the costs are stated.

### Out of scope (per ticket)
Confirm nothing here exceeds the ticket's scope:
- The operative test's five clauses are unchanged. `git diff --numstat
  60f39fb..HEAD -- docs/tier-review-model.md` gives 209 insertions and 0
  deletions at 53125cb against 60f39fb, the commit this branch was created
  from, so no line of the document that existed before this branch was
  altered; the round-1 repair, the repair after the maintainer's answer, the
  round-2 redesign and the round-3 repair rewrote only lines this branch had
  added, which `git diff --numstat 49b5c00..HEAD -- docs/tier-review-model.md`
  shows as 176 insertions and 38 deletions at 53125cb against 49b5c00, and
  `git diff --numstat 8cf72a3..HEAD -- docs/tier-review-model.md` shows as
  130 and 56 at 53125cb against 8cf72a3. The round-3 repair alone is 48
  insertions and 23 deletions on that document and 44 and 12 on ADR-0004,
  from `git diff --numstat d867af9..53125cb -- docs/tier-review-model.md
  docs/adr`.
- What each tier requires is unchanged. "The tiers" is untouched by the same
  diff, and the annotation on ADR-0002 leaves the Decision as it stands. The
  occasion added to the falsifier under R1.7 is read against this limit and
  stays inside it: it says when this rule's own falsifier is checked, which
  "Retiring a control" requires of every falsifier — "stated so that a
  reviewer could recognise it" — and it binds a reviewer already reading
  this paragraph, because this paragraph is what made the change under
  review `critical`. It adds nothing to what `critical` requires of a change
  outside this rule. The same is read of the sentence R2.5's repair adds — a
  change closed `trivial` under this line marks itself in its description.
  That binds a change closing under this rule and nothing else; it adds no
  section to `templates/PR-DESCRIPTION.md`, which lists the sections a
  description carries and not the sentences each must contain, and the
  template is untouched. The round-3 repair is read against the same limit
  and stays inside it: it says which party performs a widening of this
  paragraph's own list, and when, and it adds nothing to what `critical`
  requires of a change outside this rule.
- Tempting and deferred: the one-line summary at the foot of the section
  carries clauses 1 to 4 and not clause 5, so a contributor who reads only
  the summary gets `trivial` for a rule change. That is a defect this change
  makes more visible and does not create. It is raised as EM-007-002-001
  under §4 rather than fixed here. `docs/adr-process.md`'s wider sentence is
  raised the same way as EM-007-002-002, for the reasons stated above.

### How to verify
1. `git diff --numstat 60f39fb..HEAD -- docs/tier-review-model.md docs/adr`
   — three files at 53125cb against 60f39fb: 209 and 0 on
   `docs/tier-review-model.md`, 35 and 0 on ADR-0002, 341 and 0 on the new
   ADR-0004. 585 insertions and 0 deletions in total, derived from those
   three rows.
2. Read the whole of "The operative test" in `docs/tier-review-model.md` as
   it stands, not the diff — the reading "When review ends" asks for before
   a repair is handed back, done before this description was written, again
   after the maintainer's answer was written in, and again after the round-2
   redesign, and again after the round-3 repair. Round 1's reading
   found three defects, fixed in the same commit: the
   decision-record entry still said a record was "not a process document",
   which contradicts the definition above it now that map-named documents
   are in the class; the falsifier named "this section's parent" where it
   meant "Retiring a control"; and the falsifier did not say why a reviewer
   would have this paragraph open on the occasion it names. The reading at
   8cf72a3 found one and fixed it in the same commit: the paragraph on who
   may add to which list bound the adding of an entry to the negative list
   and said nothing about widening an entry already there, which is the act
   this very change performs. It now says the two are the same act and belong
   to the same party. The reading at d867af9 found two more, fixed in that
   same commit: that same paragraph said a widening belongs to the reviewer
   and the maintainer but never said how a reviewer performs it, so an
   executor holding a second-column must-fix against a negative-list entry
   had no route but a block — it now says the finding is the reviewer's act
   and bounds the executor to what the finding names; and the cost paragraph
   stated the hazard the maintainer accepted without saying what containment
   adds against it, which is that two documents at one commit can be read
   again by someone else. The reading at 53125cb, in the round the maintainer
   ordered on 2026-09-08, read the whole of "The operative test" and the
   whole of ADR-0004 as they now stand. It found no defect beside the repair
   and one imprecision inside it, fixed in the same commit: the repair had
   said a baseline finding goes to a retirement ticket "as an amendment with
   record", where "Retiring a control" makes retirement the default and
   amendment the option, so it now says the ticket is where widening an entry
   is an amendment with record.
3. `grep -c "^## " docs/tier-review-model.md` — 9 at 60f39fb and 9 at
   53125cb, against the nine rows of the document's index, so no section was
   added, removed or renamed.
4. `git show 60f39fb:docs/ai-contributor-policy.md | md5sum` against the
   same command at 53125cb — identical, `c98a10b7`, so the map is untouched.
   The redesign demotes that map from the entry's test to evidence, which
   changes what the entry says about the map and not the map itself.
5. `git ls-tree --name-only <commit> docs/adr/ | wc -l` — 3 at 60f39fb and 4
   at 53125cb. ADR-0004 carries `status: proposed`; `templates/ADR.md` step
   3 and ADR-0003's own line move it to `accepted` at the closing commit,
   which has not been made.
6. Check the four closures the decision leaves standing: `grep -n -i "rule
   or a procedure" docs/tickets/done/*.md`. EM-018-001, the fifth ticket
   round 1 raised, is checked by reading its closed description: it rewrote
   two steps of `templates/TICKET.md` to agree with an untouched
   `docs/ticket-lifecycle.md`, which is what the widened entry describes.
   Read against containment as the entry now states it, both worked examples
   still pass in both directions. EM-007-001's removed enumeration — ticket,
   tier, summary, criteria with evidence, out-of-scope confirmation,
   verification steps, risks and follow-ups — is a strict subset of the
   sections `grep -n "^### " templates/PR-DESCRIPTION.md` lists at 53125cb,
   and the reference it left behind states nothing the template did not.
   EM-018-001's two questions are both stated in full by the untouched
   lifecycle, and the rewritten steps say nothing it did not. No closure is
   reclassified by the redesign or by the round-3 repair: the 7 files `grep
   -l "^tier: trivial" docs/tickets/done/*.md` lists at 53125cb are the same
   7 the round-1 repair was read against, and none of them closed under this
   line.
7. `git log --format='%s%n%b' 60f39fb..HEAD` — seventeen commits at 53125cb,
   each ending in the co-authorship trailer, counted with `git log
   --oneline 60f39fb..HEAD | wc -l` and `git log --format='%b'
   60f39fb..HEAD | grep -c "Co-Authored-By: Claude Opus 5"`, which give 17
   and 17; the commit after it carries this description, and ends in it too.
8. Directory and status agree: the ticket is in `docs/tickets/active/` with
   `status: in-progress`, and the board row says `in-progress`.

### Risks / follow-ups
- **EM-007-002-001** in `docs/tickets/ready/`, proposed `critical`: the
  section's one-line summary omits clause 5.
- **EM-007-002-002** in `docs/tickets/ready/`, proposed `critical`:
  `docs/adr-process.md`, "Decisions about the process are themselves ADRs",
  states the wider reading. Raised from round 1's R1.5, with the scope
  judgement recorded above rather than made silently.
- The map in `docs/ai-contributor-policy.md` and the index in
  `docs/tier-review-model.md` needed no update, and neither was touched. No
  section was added, removed or renamed, and no question moved: the model
  already settled "What tier is my change", and it settles it still. The map
  row for decision records names the directory `docs/adr/`, and the
  map-keeping rule says a row naming a directory is what the rule keeps
  true, "not one row per file beneath it", so ADR-0004 adds no row. The
  README names ADR-0001 and ADR-0002 in prose and indexes no records; it
  does not name ADR-0003 either.
- The line's known weakness is stated in the document rather than here: the
  executor draws it at the moment the executor would prefer `trivial`. Round
  1 is the evidence that the weakness is real rather than theoretical — six
  must-fixes, most of them one class, all in the lowering direction. The
  falsifier counts the same failure after landing, and now names when it is
  counted.
- The `trivial` row of "The tiers" and the batch rule in
  `docs/ticket-lifecycle.md` both describe `trivial` work in their own
  words. Neither was edited, and neither contradicts the new line; a
  reviewer finding that one of them now reads wider than the paragraph has a
  finding, and it would be repaired in the round.
- Cost of the round-1 repair, re-measured at 53125cb: the EM-010-002 shape
  costs a round from here on, which is 1 of the 7 tickets carrying `tier:
  trivial` in `docs/tickets/done/`, read from `grep -l "^tier: trivial"
  docs/tickets/done/*.md | wc -l`; and every independent review of a
  critical-tier process-document change carries one extra read, against 19
  of the 29 closed tickets in `docs/tickets/done/` carrying `tier: critical`
  at 53125cb, read from `grep -l "^tier: critical" docs/tickets/done/*.md |
  wc -l` and `ls docs/tickets/done/*.md | wc -l`. The population that read
  covers is empty at 53125cb, now readable as empty rather than asserted:
  `grep -rl "closed trivial under the process-document line"
  docs/tickets/done/ | wc -l` gives 0 at 53125cb. None of the four figures
  moved with the redesign of d867af9 or the repair at 53125cb, neither of
  which touched a ticket file in `done/`.
- Cost of the round-2 redesign, stated with the findings it repairs. A
  containment read costs a read of one other document per corrected
  restatement, where the entry at 8cf72a3 cost a judgement about which
  document had the authority — comparable in effort and repeatable by a
  later reader, which the judgement was not. A partial restatement carrying
  anything extra returns `critical` and costs a round; so does a paragraph
  unique to the document it sits in, removed. Neither reclassifies any of
  the 7 `tier: trivial` closures at 53125cb by the command above, because
  none of them closed under this line and the two worked examples pass
  containment in both directions, re-read at 53125cb against "in full" as
  the round-3 repair defines it. Against that, the case R2.2 named — an
  adopting project with no map, correcting a restatement that cites nothing
  — costs no round where it cost one at 8cf72a3, and neither does the case
  where two documents state the same rule and neither cites the other. That
  second case is a widening beyond what the entry said at 8cf72a3, written
  because round 2's second-column must-fix names it and bounded to what that
  finding names.
- A change closed `trivial` under this line now writes one sentence about
  itself in its description, which is what makes the falsifier's population
  a set rather than the whole directory. `templates/PR-DESCRIPTION.md` is
  untouched: it lists the sections a description carries, and this is a
  sentence inside a section it already has. A reviewer that reads the
  template as owing an entry for it has a finding, and it would be repaired
  in the round.
- Cost of the maintainer's second answer, accepted with it and stated in
  ADR-0004: the exemption widens from a duplicated list to any restatement,
  and the read that decides it is made by the executor on its own work. After
  the round-2 redesign that read is containment and not a judgement about
  which document was the authority, and R3.5 is why this bullet now says so:
  the read is a cost as well as a check. It costs a read of the untouched
  document per corrected restatement; a correction carrying anything that
  document does not already say returns `critical` and pays a round; and
  where two documents state one question in full and disagree, containment
  passes while a reader of the corrected document is bound differently after
  it, which is the widest thing the entry permits and what the falsifier's
  second limb counts. "The operative test" now states that cost in its cost
  paragraph, where a contributor reads it, rather than only here and in
  ADR-0004. Nothing mechanical holds the rest; the separation-of-duties rule
  does, and the falsifier names the failure so it can be counted rather than
  argued. The direction of the risk is the one the repository has just been
  shown to run — round 1's six must-fixes were all in the lowering direction
  — which is why the widened entry is the entry the falsifier names.
- Cost of the round-3 repair, stated with the findings it repairs. A future
  second-column must-fix against an entry standing in `docs/` at the change's
  baseline now pays a round: it goes to a ticket rather than being written in
  the round. The population that pays it is 0 today, because the whole
  negative list lands in this change — 209 insertions and 0 deletions on
  `docs/tier-review-model.md` at 53125cb against 60f39fb, read from `git diff
  --numstat 60f39fb..53125cb -- docs/tier-review-model.md` — so none of the
  19 `tier: critical` closures in `docs/tickets/done/` at 53125cb can carry
  one, by the command in the bullet above. The countable omission R3.4's
  repair adds costs nothing to a closure that writes its marker sentence, and
  widens the falsifier for one that does not, which is the direction that
  raises. Neither reclassifies any closure: the 7 `tier: trivial` closures at
  53125cb are unchanged by both.

### Review

**Post-review check (2026-09-07), per `docs/quality-gates.md`, "Review
isolation":** `git status --porcelain` in this worktree returned no output,
and `git worktree list` showed twelve worktrees, none of them created by the
executor and none left behind by the review: `A:/projects/wt/review-EM-007-002`
is the reviewer's own tree, at 49b5c00 and detached, and this tree was not
written to. Nothing untracked, nothing modified, so there is no finding
against the review to record beside the round's row.

**The class of round 1**, in the form "What a review reports" asks for:
*which clause of what was written makes the maintainer's sentence operable,
and which one makes it narrower?* R1.1, R1.2 and R1.9 are instances. The
enumeration of every clause, marked raising or lowering, and what was done
with each, is in the Summary above under **The class this round repaired**.

| Round | Must-fix | Where (rules / lists / documents / tests) | Inside previous round's fix | Repaired by |
|---|---|---|---|---|
| 1 | 6 | The process-document rule in `docs/tier-review-model.md`, "The operative test": its definition sentence, its negative list and its falsifier; the decision-record reasoning in this description; `docs/adr-process.md`; the AC4 claim | — | 99e7ae7 |
| 2 | 2 | The second entry of the negative list in `docs/tier-review-model.md`, "The operative test" — both must-fixes on that one entry — and its **Retired when:** line, where the three notes sit | 2 of 2 | d867af9 |
| 3 | 1 | The same rule in `docs/tier-review-model.md`, "The operative test": the who-may-add paragraph, whose permits-direction route reaches any negative-list entry and not only one the change adds (must-fix); entry 2's two-documents carve-out, whose stated reason fails in the case it carves out; the phrase "states that question's rule or procedure in full", which reads two ways; the self-marking population of the **Retired when:** line; and this description's cost paragraph, which never states containment's read as a cost | 1 of 1 | 53125cb |

Derived from the rows above and not asserted beside them: 6 + 2 + 1 =
**nine** must-fixes over the three rounds, of which none in round 1, 2 of 2 in
round 2 and 1 of 1 in round 3 — **three** — sat inside the previous round's
fix.

**Round 4 review pending** on 53125cb. Round 3's row carries that commit
because the repair a round produces is recorded on that round's row; round 4
gets a row of its own when the round returns, and no count is asserted for it
here.

No condition of "When review ends" was satisfied in any of the three rounds,
and round 3 was the cap: the ticket blocked to the maintainer with this record
attached on 2026-09-08. The blocker is above, immediately before `## PR
Description`, and carries the per-round table appended under it as "When
review ends" requires, since the pull-request description that table would
otherwise live in is not written until close; that copy is as it stood at the
block. The maintainer ordered a fourth round on 2026-09-08, and this round is
that order. The cap is unchanged by it, and so is the record of the three
rounds.

Findings of round 1, on 49b5c00:

- R1.1 · permits · the negative list's third entry, the dated annotation ·
  it exempts an annotation "that leaves every rule and every decision as it
  stands", but the third *reaches* entry makes changing what a record
  decides `critical`, and this change's own annotation to ADR-0002 narrows
  the Context sentence's reach — remedy: the entry now reads "leaves every
  rule as it stands and changes how no decision is read"; cost: the
  EM-010-002 shape costs a round, 1 of the 7 tickets carrying `tier:
  trivial` in `docs/tickets/done/` at 99e7ae7 by the command in Risks;
  inside previous fix: no. **Must-fix, repaired at the class.**
- R1.2 · permits · the definition sentence · the class named was the
  map-keeping rule's — map-named documents plus `docs/` and `templates/` —
  so a root-level `AGENTS.md` on an adopting project fell in no category and
  came out `trivial` — remedy: the definition is by function, with the
  map-named documents added to the class rather than bounding it; cost:
  root-level policy files on adopting projects cost a round, and no document
  in this repository changes tier, since every rule-bearing document here is
  under `docs/` or `templates/` or named by the map; inside previous fix:
  no. **Must-fix, repaired at the class.**
- R1.3 · note · the same sentence · its two halves disagree, since
  `DISCLOSURE.md` is map-named and states no rules — remedy: the two tests
  are read together and neither takes anything out of the class, so a
  map-named document that states no rules stays in; taking it out would be
  lowering, which is not the executor's. **Note, taken.**
- R1.4 · permits · AC4 and the worked examples · `templates/TICKET.md`'s
  how-to-use steps are an ordered sequence a contributor performs, and
  EM-018-001 rewrote its step 5 and its step 1 and closed `standard`, so
  AC4's claim that no ticket is closed at a tier the decision contradicts
  was unsupported; the maintainer's carve-out named four tickets, not that one —
  remedy: EM-018-001 is named in AC4, and what the record does about it is
  the question of the `BLOCKER (2026-09-07)` note, because both available
  answers are the maintainer's; inside previous fix: no. **Must-fix,
  repair of the instance, and the ticket blocks on it.**
- R1.5 · permits · unreconciled documents · `docs/adr-process.md`,
  "Decisions about the process are themselves ADRs", still states the wider
  reading and was untouched and unmentioned — remedy: routed to
  EM-007-002-002 rather than annotated here, with the scope judgement stated
  in the Summary and the gap named in ADR-0004's Consequences; cost: the
  wider sentence stands until that ticket is worked, which errs `critical`
  and so raises rather than lowers; inside previous fix: no. **Must-fix,
  repair of the instance.**
- R1.6 · permits · the decision-record conclusion · the reasoning tested
  only the "Retiring a control" limb of `docs/adr-process.md` — remedy: the
  conclusion is reversed after testing both limbs against their words, and
  ADR-0004 is written per `templates/ADR.md`, created `proposed`; cost: a
  record per decision of this shape, and one more file a contributor reads
  before a first edit — four records at 99e7ae7 against three at 60f39fb;
  inside previous fix: no. **Must-fix, repair of the instance.**
- R1.7 · refuses · the **Retired when:** line · near-decorative: the
  population named was `tier: trivial` tickets in `done/`, of which none
  closed under the line, so the live population was zero; EM-017 batches
  many changes into one file; and no occasion obliged the spot-check,
  because `trivial` summons no reviewer — remedy: the line names the
  occasion (every independent review of a critical-tier process-document
  change), the command that lists the population, and the population as
  changes rather than tickets, stated empty at landing; cost: one extra read
  per such review, against 19 of the 29 closed tickets carrying `tier:
  critical` at 99e7ae7 by the commands in Risks; inside previous fix: no.
  **Must-fix, repair of the instance.**
- R1.8 · note · the line generally · it does leave ordinary work `trivial`
  — six of the seven closures still return `trivial`, and the fourth
  negative entry holds "a procedure" back. **Note, taken, and its count
  moves down by one with the repair of R1.1.** The seven tickets carrying
  `tier: trivial` in `docs/tickets/done/` at 99e7ae7 are EM-007-001,
  EM-010-002, EM-012-001-001, EM-016-001, EM-016-001-001, EM-017 and
  EM-019, read from `grep -l "^tier: trivial" docs/tickets/done/*.md`. Of
  those, EM-010-002 returns `critical` under the line as repaired, because
  it annotated ADR-0002 to change how two of its sentences are read — the
  cost R1.1 states. The note's substance is untouched by that: what holds
  ordinary work at `trivial` is the fourth negative entry for a wording
  change and the `trivial` row of "The tiers" for an edit to a ticket file,
  which is not a process document at all. No recomputed total is asserted
  here, because the falsifier's population counts changes and not tickets,
  and EM-017 is a batch.
- R1.9 · note · beyond the maintainer · the maintainer's answer was one
  sentence and the change decided more than that sentence, in the direction
  that lowers — taken as the class of the round; see **The class this round
  repaired**. **Note, taken as the class.**

After the round, on its own lines:

- **R1.4, routed and answered.** The question R1.4 left open was routed to
  the maintainer under the contributor policy's §3 on 2026-09-07 and answered
  the same day: the line does not reach a change that corrects a restatement
  of a rule or a procedure to agree with an unchanged document that settles
  it, and such a change is `trivial`. The answer, its reasoning and the cost
  it accepts are in Notes above and in ADR-0004; the repair that writes it
  into `docs/tier-review-model.md` is 8cf72a3. EM-018-001's `standard`
  closure stands and EM-007-001 keeps its `trivial` closure, so no ticket
  closed before this change sits at a tier the decision contradicts.
- **Post-review check, re-run at 8cf72a3 (2026-09-07)**, per
  `docs/quality-gates.md`, "Review isolation": `git status --porcelain`
  returned no output and `git worktree list` showed twelve worktrees, none
  created by the executor and none left by the review;
  `A:/projects/wt/review-EM-007-002` is the reviewer's own tree, still at
  49b5c00 and detached, and this tree was not written to. Nothing untracked,
  nothing modified, so there is no finding against the review.

**The class of round 2**, in the form "What a review reports" asks for:
*the entry decided a tier from a relationship between two documents — which
one settles the question — and that relationship is not a fact the change
carries.* R2.1 and R2.2 are the two faces of it, one in each direction. The
redesign, the six siblings the question enumerates and what a reader does
differently for each are in the Summary above under **The class round 2
repaired**.

**The class signal fired, and the adjustment was refused.** Round 1's R1.4
was a first-column finding on this entry; round 2's R2.2 is a second-column
finding on the same entry, inside R1.4's fix. That is the signal
`docs/tier-review-model.md`, "What a review reports", names, and its rule is
that the repair is a redesign against the class and not a further
adjustment. The reviewer named the signal and recorded beside it, without
proposing it, the adjustment it would otherwise have offered: *let deference
answer where no map exists anywhere, and where nothing defers let the
executor record which document it treated as settling and take `trivial`*.
That adjustment is **refused**. It is a third adjustment to the same clause
on the same question, and it leaves R2.1 standing — a recorded judgement
about which document was settling says nothing about what left the
documents, so text unique to the restatement could still be deleted at
`trivial`. What was written instead is the redesign above: containment,
answered from the change and the documents rather than from their standing
relationship, which answers both findings from one test and needs no
recorded judgement at all. The refusal is carried in the decision record as
ADR-0004's Alternative 6, so that a later reader meets it where the decision
is, and so that the signal's own falsifier — three redesigns whose effect is
the adjustment refused — has a case it can read.

**Repairs of repairs, 2 of 2.** Both round-2 must-fixes sit inside round 1's
fix, so the proportion signal in "When review ends" fires as well as the
single-rule one. Both point at the same repair and both are answered by the
one redesign; the round's repair is that redesign and not two per-finding
patches.

Findings of round 2, on 8cf72a3:

- R2.1 · permits · "The operative test", negative list entry 2, "corrected,
  or replaced outright by a reference to it" · no containment guard: text
  unique to the restatement could be deleted at `trivial` by calling the
  paragraph a restatement, because the old wording — "a *list duplicated*
  from another document" — made containment definitional and the widening
  dropped it; that is content removal and not the
  which-document-was-the-authority cost the maintainer accepted — remedy:
  the entry requires that the untouched document already state everything
  the corrected or replaced text stated, and says that removing text it does
  not carry retires a rule or a procedure and is reached by the bold words;
  cost: a containment read of that document, and a partial restatement
  carrying anything extra returns `critical`; it reclassifies none of the 7
  tickets carrying `tier: trivial` in `docs/tickets/done/` at d867af9 by the
  command in Risks, since EM-007-001's removed enumeration is a strict
  subset of the sections `templates/PR-DESCRIPTION.md` lists; inside
  previous fix: yes (R1.4). **Must-fix, repaired at the class.**
- R2.2 · refuses · same entry, "where two documents state the same rule and
  neither defers to the other … the change is answered by the bold words
  above — which raises" · the map is this repository's own artefact; on an
  adopting project with no map, a restatement that does not itself cite its
  source has no settling document, so every such correction returned
  `critical` and cost a round — the class of work the decision exists to
  keep cheap — remedy: containment replaces the relationship, deference and
  the map become evidence for finding the document rather than the test, and
  where two documents state the same question in full and neither cites the
  other either is the untouched document for a correction of the other;
  cost: the entry reaches further than it did at 8cf72a3 in exactly the two
  cases the finding names, and that reach is a lowering, written because the
  reviewer's second-column must-fix names it and bounded to what it names;
  inside previous fix: yes. **Class signal named. Must-fix, repaired by
  redesign at the class.**
- R2.3 · note · same entry, "the document the restatement itself defers to,
  **by naming it** or by citing it as the authority" · "naming it" is looser
  than deference and let a mere mention supply a settling document off-repo,
  which lowers — **taken, and it falls out of the redesign**: the clause is
  gone with the test it qualified, and a citation now points a reader at a
  document to check rather than settling anything by itself. Inside previous
  fix: yes.
- R2.4 · note · **Retired when:**, the "Including" clause · its named
  failure — a contributor afterwards found to have performed the restatement
  — is evidence about contributor behaviour, which the stated occasion, a
  reviewer reading `tier: trivial` closures in `done/`, does not supply —
  **taken**: the **Including** clause now names the containment failure,
  which two documents at one commit do supply, and the
  contributor-behaviour failure is stated separately and counted where it
  surfaces, from a `BLOCKER:` raised under the contributor policy's §3 or a
  review finding, with the falsifier saying that nobody is obliged to go
  looking for it. Both count toward the same "more than once", so the
  falsifier is wider than it was, which is the safe direction the note
  names. Inside previous fix: yes (R1.7).
- R2.5 · note · **Retired when:**, the population command · `grep -l "^tier:
  trivial" docs/tickets/done/*.md` lists every `trivial` closure and not the
  subset closed under this line, which was empty at landing, and the filter
  was stated in words with no field marking it, so the read grew with the
  directory — 7 files at 8cf72a3 — **taken**: a change closed `trivial`
  under this line marks itself in its pull-request description with the
  sentence *closed trivial under the process-document line*, and the
  reviewer lists the population with `grep -rl "closed trivial under the
  process-document line" docs/tickets/done/`, which returns 0 files at
  d867af9 against the 7 the old command returns there. The population now
  grows with this line rather than with the directory, at the cost of one
  sentence per closure. Inside previous fix: yes (R1.7).

After the round, on its own lines:

- **The whole-section read at d867af9**, per "When review ends", "The repair
  is read whole before it is handed back": the whole of "The operative test"
  and the whole of ADR-0004 were read as they now stand. Two defects beside
  the repair were found and fixed in the same commit; both are described in
  step 2 of How to verify.
- **Post-review check after round 2 (2026-09-08)**, per
  `docs/quality-gates.md`, "Review isolation": `git status --porcelain` in
  this worktree returned no output before any edit was made, and `git
  worktree list` showed twelve worktrees, none created by the executor and
  none left behind by the review; `A:/projects/wt/review-EM-007-002` is the
  reviewer's own tree, at 3c7b5b5 and detached, and this tree was not
  written to. Nothing untracked, nothing modified, so there is no finding
  against the review to record beside the round's row.

**Round 3's independent verification, recorded before its findings.** The
reviewer tested the redesign rather than accepting it, and reports it genuine:
the judgement moves from an unwritten relationship between two documents to
two documents at one commit, and it needs no map, no deference and no
repository-specific artefact. Four cases were constructed and worked:

- a partial restatement fails the question-granular "in full" and returns
  `critical`, with granularity self-correcting upward;
- a typo in a passage the other document does not carry passes, though the
  interaction between entry 2 and entry 4 is left unstated;
- a settling document changed in the same commit fails "not touched by the
  same change", determinately;
- two documents each containing the other is answered by the entry, and the
  answer lowers.

R2.1's containment guard holds and the deletion door does not reopen. Every
clause of the paragraph raises or is neutral except the two siblings the
remedy recorded with R2.2 named. Every figure this description states was
reproduced from its own command: 0 files matching the marker sentence against
the 7 in `docs/tickets/done/` carrying `tier: trivial`; 19 of the 29 closed
tickets carrying `tier: critical`; 9 `##` sections in
`docs/tier-review-model.md` at both commits; four decision records at d867af9
against three at 60f39fb; three annotations on ADR-0002 against two; the
numstat figures 184/0, 151/38 and 105/56; 13 commits carrying 13
`Co-Authored-By` trailers; and the contributor policy identical by md5 at both
commits, with the map and the index correctly untouched.

**The falsifier discharged on this occasion.** The occasion the **Retired
when:** line names is every independent review of a critical-tier
process-document change, and this round is one. `grep -rl "closed trivial
under the process-document line" docs/tickets/done/` returned 0: the population
is empty, and there was nothing to read.

**The class of round 3**, in the form "What a review reports" asks for:
*which routes does this change give an executor to change a control that
constrains it?* R3.1 is the instance the reviewer found, and it is a
separation-of-duties defect: the sentence it lands on let an executor widen,
inside the round, an entry that had refused its own work. The whole change
was swept for routes of that shape. Ten were found and are enumerated in the
Summary above under **The class round 3 repaired**, each with whether it is
bounded correctly and what a reader does differently: adding to the *reaches*
list; adding to the negative list; widening an entry already there; the
in-round widening a second-column must-fix authorises; who works the ticket
that widening otherwise takes; the marker sentence that puts a closure in the
falsifier's population; the containment read itself; the falsifier's
occasion; the line's own **Retired when:**; and the dated-annotation entry.
Two were not bounded — the fourth, which is R3.1, and the sixth, which is
R3.4's note — and both are repaired at 53125cb. All three of the repairs
tighten, so all three were the executor's to write.

Findings of round 3, on a82d795:

- R3.1 · permits · "The operative test", the who-may-add paragraph, the
  sentence added at `d867af9` ("The reviewer performs the act by recording
  it…") · as written the route reaches a second-column must-fix against **any**
  negative-list entry and not only one the change under review adds, so a
  future executor whose own work an entry refused could widen that entry in
  the round — which "Retiring a control" routes to a retirement ticket as an
  amendment with record, its bullet 4 being the one that reaches a finding not
  matching the line's permits-direction falsifier, and which that section
  closes with "A retirement ticket is not worked by the executor whose work
  the rule refused"; the trailing citation also over-claims, since bullet 2
  covers only a finding *matching* the falsifier of a rule the change adds —
  remedy: bound the route to an entry the change under review itself adds,
  leaving a pre-existing entry to the ticket and the round the preceding
  sentence already names; cost of the tightening: a future second-column
  must-fix on a baseline entry pays a round, over a population of 0 today,
  since the whole list lands in this change — 184 insertions and 0 deletions,
  read from `git diff --numstat 60f39fb..d867af9 -- docs/tier-review-model.md`
  — so none of the 19 `tier: critical` closures in `docs/tickets/done/` can
  carry one, re-measured at the repair as 209 and 0 from `git diff --numstat
  60f39fb..53125cb -- docs/tier-review-model.md` with the same 19 closures;
  inside previous fix: yes (R2.2's, beside it). **Must-fix, repaired at the
  class in the round the maintainer ordered on 2026-09-08 — see The class
  round 3 repaired, whose sweep of the whole change for routes of this shape
  found ten and two unbounded.**
- R3.2 · permits · negative list entry 2, "Where two state it in full and
  neither cites the other, either is the untouched document" · where the two
  documents disagree, a reader of the edited document *is* bound differently
  after the change, so the entry's stated reason — that what a contributor is
  bound to do is as it was — does not hold in the one case the entry carves
  out; the falsifier's second limb counts that case and the entry does not say
  so — remedy: one clause, in the entry or in the cost paragraph; inside
  previous fix: yes (R2.2). **Note, taken:** the entry now says that where the
  two disagree containment still passes while a reader who had been following
  the corrected document is bound differently after it, that the reason the
  entry rests on holds for the documents and not for that reader, and that
  this is what the falsifier's second limb counts. The cost bullet in Risks
  and ADR-0004's Consequences say the same. Nothing is reclassified: the case
  returned `trivial` before the clause and returns `trivial` after it, and
  what changed is that the entry states what it is permitting.
- R3.3 · permits · "states that question's rule or procedure in full" · the
  phrase carries two readings, text-containment and topic-coverage, and only
  the first keeps "what is unique to it is not a copy" coherent; "the
  rewritten sentences" is used pre-state in one bullet and post-state in the
  other — remedy: define "in full" as saying everything the removed text said;
  inside previous fix: yes (R2.1). **Note, taken:** "in full" is now text
  containment — the untouched document says everything the text the change
  removes said, and not merely that it covers the same subject — and the two
  halves of the test name the sentences as they answered before the change and
  as they say after it. ADR-0004's Decision carries the same definition. It
  raises: the topic-coverage reading was the looser of the two.
- R3.4 · permits · the **Retired when:** line, the self-marking population ·
  the marker sentence is written by the party the control is on, so a closure
  wrongly claiming `trivial` that omits it is outside the read, and the
  falsifier does not make the omission itself countable — remedy: one
  sentence; inside previous fix: yes (R2.5). **Note, taken as a sibling of the
  round's class**, since a marker the controlled party may omit is a route of
  exactly the shape R3.1 names: a closure found to have taken this line
  without the sentence now counts toward the same "more than once", counted
  where it surfaces, whatever that closure altered. Cost: nothing to a closure
  that writes its sentence; the falsifier is wider for one that does not,
  which is the direction that raises.
- R3.5 · refuses · this description's cost paragraph · containment's read is
  named but never as a cost; it is stated only in ADR-0004 and under Risks /
  follow-ups — remedy: state it as a cost where the costs are stated; inside
  previous fix: not recorded by the reviewer, and transcribed here as the
  absence it is rather than resolved. **Note, taken in both places:** the cost
  paragraph of "The operative test" now states the containment read as a cost
  — a read of the untouched document per corrected restatement, and `critical`
  and a round for a correction carrying anything that document did not already
  say — beside what it already said the read is worth; and the Risks bullet
  naming the second answer's cost is restated in the redesign's terms, where
  it still described the authority judgement the redesign replaced.

After the round, on its own lines:

- **No condition of "When review ends" was met by round 3.** Not condition 1:
  the round found a must-fix. Not condition 2: R3.1 lies inside no limit this
  ticket records, since Out of scope records only the operative test's five
  clauses and what each tier requires, and R3.1 sits inside neither. Not
  condition 3: it adds no entry to an enumeration maintained against an
  adversary. Round 3 of a cap of three, so the ticket blocks to the maintainer
  with this record attached — which "When review ends" states is a success
  path in exactly the sense of the contributor policy's §3, the executor
  having identified that the loop is not converging rather than taking another
  round that looks like progress. Nothing in round 3 was repaired, and the
  table's last column says so.
- **The class signal did not fire on R3.1, and the reviewer records why.**
  R3.1 lands on a different rule from R2.2, and its direction is
  second-column then first-column, which the signal's words in "What a review
  reports" do not name: the signal is written for a first-column finding
  followed in the next round by a second-column one. The reviewer flags that
  as worth the maintainer's eye. The blocker above carries it, together with
  the second instance recorded on another project, as fact rather than as a
  proposal.
- **Post-review check after round 3 (2026-09-08)**, per
  `docs/quality-gates.md`, "Review isolation", made before the first edit of
  this round: `git status --porcelain` in this worktree returned no output,
  and `git worktree list` showed twelve worktrees, none created by this
  ticket's executor and none left behind by the review;
  `A:/projects/wt/review-EM-007-002` is the reviewer's own tree, at a82d795
  and detached, and this tree was not written to. Nothing untracked, nothing
  modified, so there is no finding against the review to record beside the
  round's row.
- **Post-review check re-run before the first edit of the ordered round
  (2026-09-08)**, per the same rule, at 73ff02c and before the unblock:
  `git status --porcelain` returned no output and `git worktree list` showed
  the same twelve worktrees, none created by this ticket's executor and none
  left behind by the review, with `A:/projects/wt/review-EM-007-002` still at
  a82d795 and detached. Nothing untracked, nothing modified, so there is no
  finding against the review to record beside round 3's row.
- **The whole-section read at 53125cb**, per "When review ends", "The repair
  is read whole before it is handed back": the whole of "The operative test"
  and the whole of ADR-0004 were read as they now stand. Nothing was found
  beside the repair, and one imprecision inside it was fixed in the same
  commit — step 2 of How to verify describes it.
- **The reviewer's observation about the class signal's wording stays with
  the maintainer.** Round 3 recorded, as fact and not as a proposal, that the
  signal in "What a review reports" did not fire on R3.1 and why, and that a
  second instance of the same gap exists on another project, so the bar in "A
  rule needs a second instance" is met. The blocker above carries it. The
  order of 2026-09-08 is for a round taking R3.1 and the four notes, and
  names no rule; whether a rule is written, and in what words, is the
  maintainer's to direct, so nothing is written for it here.
