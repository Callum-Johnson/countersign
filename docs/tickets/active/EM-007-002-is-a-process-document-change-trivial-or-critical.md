---
id: EM-007-002
title: A change to a process document is trivial by the operative test and critical by ADR-0002
status: in-progress
tier: standard
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

**BLOCKER (2026-09-08):** the round the maintainer ordered is complete — the
repair at 53125cb and its independent review — and the review recorded **three
must-fixes**. None is repaired. A further round is the maintainer's to order,
as the fourth was: the cap in `docs/tier-review-model.md`, "When review ends",
stands at three, and applying these remedies here would take a fifth round
that nobody has ordered. The full round-4 record, with the reviewer's
independent verification and its commands, is in the Review section of the
description below, which travels with this block.

**The three must-fixes, with their remedies, deliberately not applied.**

- **R4.1, first column.** The who-may-add paragraph's closing gloss sends a
  finding against a baseline entry to "the retirement ticket … where widening
  an entry is an amendment with record". "Retiring a control" grants no such
  permission: it allows amendment only where the match is technical and the
  correction small, requires the decision record to say why the match was
  technical, and makes retirement the default — and neither of its
  second-column bullets contemplates widening the *entry*, the fourth widening
  the *falsifier*. The remedy is to name the retirement ticket and let that
  section choose, at a cost of 0 changes today, since the whole negative list
  lands in this change: 209 insertions and 0 deletions on
  `docs/tier-review-model.md` at 53125cb against 60f39fb, from `git diff
  --numstat 60f39fb..53125cb -- docs/tier-review-model.md`, and none of the 19
  `tier: critical` closures in `docs/tickets/done/` at 53125cb carries one.
- **R4.2, first column.** Negative list entry 2 says that where two documents
  disagree, "containment still passes — every question is still answered in
  full", which the same commit's R3.3 repair contradicts: **Nothing left** now
  demands that the untouched document say everything the removed text said and
  not merely cover the same subject, and a disagreeing document does not. The
  clause states the reading R3.3 excluded, and it returns `trivial` where the
  test as repaired returns `critical` — so an executor may correct alone, at
  `trivial`, a document that binds it. ADR-0004 carries both readings, at L108
  and L217. The remedy is that the case fails **Nothing left**, so the entry
  does not apply to it; the cost is a round for that case, 0 of the 7 `tier:
  trivial` closures at 53125cb are affected, and both worked examples are
  unaffected.
- **R4.3, second column.** The same paragraph routes a finding to a retirement
  ticket "whatever column the finding falls in. It goes to the ticket and the
  round". A first-column must-fix on a baseline entry says the entry is too
  wide and is therefore narrowed, which raises, and raising is the executor's
  own direction under "Separation of duties"; "Retiring a control" routes only
  second-column findings there. The remedy is to bar in-round *widening* and
  drop "whatever column", at no cost.

**The no-block reasoning failed.** Round 4 declined to block on the ground
that *every repair tightens, and tightening is the executor's direction*. That
claim was made, and it was wrong: R4.1 and R4.2 loosen. In the reviewer's
words, **round 1's failure recurred** — round 1's entire finding on this
ticket was an executor lowering a tier while believing it had not, and the
same thing has happened again, this time under an explicit claim to the
contrary. That is the fact the maintainer is asked to weigh before deciding
what happens next, because it is the one thing the record now shows twice.

**The class signal fired, and this time the wording matched without strain.**
R3.1 was a first-column finding on the who-may-add paragraph; R4.3 is a
second-column finding on the same paragraph, inside R3.1's fix. The reviewer
records explicitly that this is **not** a fifth near-miss: the signal in "What
a review reports" worked as written, with nothing stretched to make its words
reach. That belongs beside the near-misses of the same wording already on
record — four of them by the reviewer's count, this ticket's R3.1 and the
OMN-022-003 instance among them — because it is evidence about when the
wording holds rather than only about when it does not, and the second-instance
bar recorded in the blocker above was met on the failures alone. The
repairs-of-repairs signal in "When review ends" fires as well, 3 of 3 inside
round 3's fix.

**The ten-route sweep was short; the corrected count is thirteen.** Route 11
is R4.2, unbounded and in the diff. Routes 12 and 13 — the bold-words read and
the process-document-definition read, which R4.5 names — are bounded but were
unnamed. Of the ten already recorded, routes 1 to 3 and 7 to 10 are genuinely
bounded, routes 4 and 5 hold, and route **6 does not**, which is R4.4: an
omitting closure still leaves the readable population, and only the count
widens.

**The trend the decision turns on.** Must-fixes ran 6, 2, 1, 3 across the four
rounds — twelve in total, derived from the per-round table below and not
asserted beside it. Six of those twelve sat inside a previous round's fix:
both of round 2's, inside round 1's repair; round 3's single one, inside round
2's; and all three of round 4's, inside round 3's. The count fell for three
rounds and rose again in the round that was meant to close the ticket, and
half the must-fixes on the record are now repairs of repairs.

**The reviewer's verdict on the ordered round: justified.** It repaired a real
rule defect and exposed three more in the operative test, so the cap's own
**Retired when:** line in "When review ends" — a ticket blocked at the cap
whose maintainer orders a further round that finds a rule defect — is matched
by this case. The reviewer also judged the round-table deviation correct: the
record asks for "the commit that repaired it", 53125cb repaired round 3, and a
round-4 row written at the block would have asserted a count for a review that
had not run; the derived total was 9 either way, three inside previous fixes,
and each round's reviewed commit is readable from its findings heading. Round
4 now carries a row of its own.

The per-round record travels with the block, as "When review ends" requires,
because the pull-request description it would otherwise live in is not written
until close. It repeats the table in the Review section below rather than
pointing at it, so a reader of the blocker needs nothing else:

| Round | Must-fix | Where (rules / lists / documents / tests) | Inside previous round's fix | Repaired by |
|---|---|---|---|---|
| 1 | 6 | The process-document rule in `docs/tier-review-model.md`, "The operative test": its definition sentence, its negative list and its falsifier; the decision-record reasoning in this description; `docs/adr-process.md`; the AC4 claim | — | 99e7ae7 |
| 2 | 2 | The second entry of the negative list in `docs/tier-review-model.md`, "The operative test" — both must-fixes on that one entry — and its **Retired when:** line, where the three notes sit | 2 of 2 | d867af9 |
| 3 | 1 | The same rule in `docs/tier-review-model.md`, "The operative test": the who-may-add paragraph, whose permits-direction route reaches any negative-list entry and not only one the change adds (must-fix); entry 2's two-documents carve-out, whose stated reason fails in the case it carves out; the phrase "states that question's rule or procedure in full", which reads two ways; the self-marking population of the **Retired when:** line; and this description's cost paragraph, which never states containment's read as a cost | 1 of 1 | 53125cb |
| 4 | 3 | The same rule in `docs/tier-review-model.md`, "The operative test", every finding inside round 3's own fix: the who-may-add paragraph's closing gloss, which sends a baseline finding to "the retirement ticket … where widening an entry is an amendment with record", a permission "Retiring a control" does not grant (must-fix); the same paragraph's "whatever column the finding falls in. It goes to the ticket and the round", which routes a first-column must-fix to a retirement ticket (must-fix); negative list entry 2's "Where the two disagree, containment still passes", which states the topic-coverage reading the same commit's R3.3 repair excluded (must-fix); route 6 of round 3's sweep; the sweep's own coverage; and the fall-through from entry 2 for a typo-fixing correction | 3 of 3 | — |

Derived from the rows: 6 + 2 + 1 + 3 = twelve must-fixes over the four rounds,
of which 2 + 1 + 3 = six sat inside the previous round's fix. Round 4's `—` in
the last column is nothing repaired, which is the point of the block.

**Discharged (2026-09-10) by the maintainer's answer recorded here. The
blocker text above is left as the record of why the work stopped.** The
maintainer did not order a fifth round and did not accept the record as it
stood; the question the Specification carried was answered again, replacing
the answer of 2026-09-07 before it landed:

> A process-document change is **`standard`**: one independent review pass,
> closing on that pass. **The executor may not raise it** to `critical`.
> Neither trivial by the operative test nor critical by ADR-0002.

The reasoning recorded with the answer: the raise-never-lower rule plus
critical-by-default drove every documentation ticket into the full loop —
EM-024 ran four independent passes on prose — and the loop's cost on
documents was disproportionate to what it caught. The decision is to get the
project back to product work and stop prose-based error rounds.

What follows from it here: the line written under the answer of 2026-09-07
does not land; the rule that lands is the answer above, with the tier of a
process-document change fixed at `standard` and its review fixed at one pass;
R4.1 to R4.3 are not repaired, since the text they land on is replaced; and
this ticket is worked under its own answer, at `standard`, on one pass, per
the Tier section below. The per-round record of the four passes stands in
the Review table below as it was recorded.

## PR Description

### Ticket
EM-007-002 — A change to a process document is trivial by the operative test
and critical by ADR-0002

### Tier
`standard` — this change is to process documents and is worked under its own
answer: one independent review pass, closing on that pass, and the executor
does not raise it. Rows 1 to 4 of the Review table are the `critical`-tier
passes taken under the answer of 2026-09-07, before the tier was fixed; the
pass this tier requires is row 5, on the head this description names, and it
is not the executor's to run.

### Summary
A change to a process document is `standard`, reviewed in one independent
pass and closed on it, and the executor may not raise it.
`docs/tier-review-model.md`, "The operative test", states the rule and its
falsifier at 8eb0f83; ADR-0004 records the decision with the text it
replaces, and every other document that states the tier of a
process-document change says the same thing.

### Acceptance criteria
- [x] AC1: `docs/tier-review-model.md` states when a change to a process
  document is `critical` and when it is `trivial` — neither: the paragraph
  beginning **A change to a process document** in "The operative test" at
  8eb0f83 says `standard`, one pass, not raised by the executor.
- [x] AC2: the statement and ADR-0002 agree — the annotation dated
  2026-09-10 at the end of `docs/adr/0002-*.md` narrows the Context
  sentence's reach, and ADR-0004, Decision, "Text amended under this
  decision", carries each amended line as it stood and as it now reads, per
  `docs/adr-process.md`, "When to write one". `docs/adr-process.md`,
  "Decisions about the process are themselves ADRs", matched its own
  **Retired when:** line and is amended in place under "Retiring a
  control", "Amendment with record"; the match is technical — one tier word
  in its second sentence, the first sentence and the argument unchanged.
- [x] AC3: the rule carries a **Retired when:** line — `grep -c 'closed on
  one pass under this paragraph' docs/tier-review-model.md` returns 1 at
  8eb0f83.
- [x] AC4: the tickets `grep -L '^tier: standard' docs/tickets/done/*.md`
  lists at 8eb0f83, less those whose change touched no process document —
  a read of each — closed at a tier the answer would not now assign. The
  record leaves every one as it stands: ADR-0004, Decision, last paragraph,
  and Migration; the answer binds from 2026-09-10 forward.
- [ ] AC5: written as "critical tier per ADR-0002"; under the answer it is
  the one independent pass, in two columns, recorded as row 5 of the Review
  table. Discharged when that pass has run.

### Falsification
N/A — no suite. Per criterion, what a reader does differently:
- AC1 — a contributor changing a process document files it `standard`, asks
  for one pass, closes on it, and does not raise it.
- AC2 — a reader of ADR-0002's Context sentence reaches the annotation and
  does not conclude a process-document change is `critical`; a reader of
  `docs/adr-process.md` is told a process change gets one pass, not a loop.
- AC3 — a reviewer meeting a process-document change closed on one pass that
  turns out to have touched what a program executes records it against that
  line rather than against the change alone.
- AC4 — a reader auditing a closed ticket at `trivial` or `critical` finds
  it not reclassified, and the reason in ADR-0004.
- AC5 — the reviewer runs one pass; the executor repairs or routes its
  must-fixes and closes rather than handing back.

### Out of scope (per ticket)
- The five clauses are unchanged: `git diff 60f39fb..HEAD --
  docs/tier-review-model.md | grep -c '^[-+][0-9]\. \*\*'` returns 0 at
  8eb0f83. Clause 5's "a change to the review model itself" is read with the
  paragraph, which says so; the clause's words are a risk below.
- What each tier requires: the `standard` row of "The tiers" now carries the
  one pass the answer gives a process document. That is the answer's own
  content, recorded in ADR-0004 as an amended line, not a change this ticket
  chose.

### How to verify
1. `git diff --stat 60f39fb..HEAD -- docs templates README.md` — every file
   this branch touches, at 8eb0f83.
2. Read whole, as they stand: "The operative test", "The tiers", "Separation
   of duties" and "Retiring a control" in `docs/tier-review-model.md`;
   ADR-0004; the last annotation of ADR-0002 and of ADR-0003; "Decisions
   about the process are themselves ADRs" in `docs/adr-process.md`; §6 of
   `docs/ai-contributor-policy.md`; step 3 of `templates/TICKET.md`; core
   idea 4 of `README.md`. Each says `standard`, one pass, not raised.
3. `grep -rn 'classifies as .critical\|critical tier under the
   process-surface' docs templates README.md | grep -v docs/tickets/`
   returns only ADR-0004's quotations of the text as it stood, at 8eb0f83;
   ADR-0002's own Context sentence stands unquoted above its annotation.

### Risks / follow-ups
- Clause 5 of the operative test still names "a change to the review model
  itself" as `critical`; the paragraph beneath reads the item with itself,
  and amending the clause's words is outside this ticket. The pass says
  whether that read holds.
- EM-007-002-001 stands in part, at `standard`: the summary's `critical`
  limb still omits clause 5 for a CI configuration change and a schema
  migration; its process-document limb is written here. Its Notes say which
  half stands.
- EM-007-002-002 is closed unworked in `docs/tickets/done/`, mooted: the
  sentence it would have reconciled matched its own falsifier and is amended
  here with record.
- A typo fix to a process document now takes a ticket and a pass, and the
  batch path does not carry it. ADR-0004, Consequences, names the cost; it
  is the answer's.

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
with each, is in the Summary of this description at a0adb0b under **The class
this round repaired**.

| Round | Must-fix | Where (rules / lists / documents / tests) | Inside previous round's fix | Repaired by |
|---|---|---|---|---|
| 1 | 6 | The process-document rule in `docs/tier-review-model.md`, "The operative test": its definition sentence, its negative list and its falsifier; the decision-record reasoning in this description; `docs/adr-process.md`; the AC4 claim | — | 99e7ae7 |
| 2 | 2 | The second entry of the negative list in `docs/tier-review-model.md`, "The operative test" — both must-fixes on that one entry — and its **Retired when:** line, where the three notes sit | 2 of 2 | d867af9 |
| 3 | 1 | The same rule in `docs/tier-review-model.md`, "The operative test": the who-may-add paragraph, whose permits-direction route reaches any negative-list entry and not only one the change adds (must-fix); entry 2's two-documents carve-out, whose stated reason fails in the case it carves out; the phrase "states that question's rule or procedure in full", which reads two ways; the self-marking population of the **Retired when:** line; and this description's cost paragraph, which never states containment's read as a cost | 1 of 1 | 53125cb |
| 4 | 3 | The same rule in `docs/tier-review-model.md`, "The operative test", every finding inside round 3's own fix: the who-may-add paragraph's closing gloss, which sends a baseline finding to "the retirement ticket … where widening an entry is an amendment with record", a permission "Retiring a control" does not grant (must-fix); the same paragraph's "whatever column the finding falls in. It goes to the ticket and the round", which routes a first-column must-fix to a retirement ticket (must-fix); negative list entry 2's "Where the two disagree, containment still passes", which states the topic-coverage reading the same commit's R3.3 repair excluded, and which ADR-0004 carries at L108 beside the excluding reading at L217 (must-fix); route 6 of round 3's sweep, whose repair widens a count and does not bound the route; the sweep's own coverage; and the fall-through from entry 2 for a typo-fixing correction | 3 of 3 | — |

Derived from the rows above and not asserted beside them: 6 + 2 + 1 + 3 =
**twelve** must-fixes over the four rounds, of which none in round 1, 2 of 2
in round 2, 1 of 1 in round 3 and 3 of 3 in round 4 — **six** — sat inside the
previous round's fix.

Rows 1 to 4 were taken at `critical` under the answer of 2026-09-07. R4.1 to
R4.3 are not repaired: the text they land on is replaced at 8eb0f83, per the
discharge note of 2026-09-10 in Notes. Row 5 is the one pass this ticket's
tier requires, and is added by that pass.

Round 4's `—` in the last column is nothing repaired. Its three must-fixes are
recorded and none is applied: a fifth round is the maintainer's to order, and
writing the remedies here would take one. Round 3's row carries 53125cb
because the repair a round produces is recorded on that round's row, and
53125cb is also the commit round 4 read.

No condition of "When review ends" was satisfied in any of the four rounds.
Round 3 was the cap: the ticket blocked to the maintainer with this record
attached on 2026-09-08, and that blocker is above, immediately before `## PR
Description`, carrying the per-round table appended under it as "When review
ends" requires, since the pull-request description that table would otherwise
live in is not written until close; that copy is as it stood at the block. The
maintainer ordered a fourth round the same day, and round 4 is that order. The
cap is unchanged by it, and so is the record of the three rounds. Round 4
returned three must-fixes and none is repaired, so the ticket blocks again, on
the second blocker of 2026-09-08 immediately before `## PR Description`, which
carries the table as it now stands with round 4's row on it.

Findings of round 1, on 49b5c00:

- R1.1 · permits · the negative list's third entry, the dated annotation ·
  it exempts an annotation "that leaves every rule and every decision as it
  stands", but the third *reaches* entry makes changing what a record
  decides `critical`, and this change's own annotation to ADR-0002 narrows
  the Context sentence's reach — remedy: the entry now reads "leaves every
  rule as it stands and changes how no decision is read"; cost: the
  EM-010-002 shape costs a round, 1 of the 7 tickets carrying `tier:
  trivial` in `docs/tickets/done/` at 99e7ae7 by `grep -l "^tier: trivial" docs/tickets/done/*.md | wc -l`;
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
  in the Summary and the gap named in ADR-0004's Consequences, both at a0adb0b; cost: the
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
  critical` at 99e7ae7 by `grep -l "^tier: critical" docs/tickets/done/*.md |
  wc -l` and `ls docs/tickets/done | wc -l`; inside previous fix: no.
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
differently for each are in the Summary of this description at a0adb0b under
**The class round 2 repaired**.

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
  tickets carrying `tier: trivial` in `docs/tickets/done/` at d867af9 by
  `grep -l "^tier: trivial" docs/tickets/done/*.md | wc -l`, since EM-007-001's removed enumeration is a strict
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
  step 2 of How to verify at a0adb0b.
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
Summary of this description at a0adb0b under **The class round 3 repaired**,
each with whether it is
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
  and ADR-0004's Consequences, both at a0adb0b, say the same. Nothing is reclassified: the case
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
  commit — step 2 of How to verify at a0adb0b describes it.
- **The reviewer's observation about the class signal's wording stays with
  the maintainer.** Round 3 recorded, as fact and not as a proposal, that the
  signal in "What a review reports" did not fire on R3.1 and why, and that a
  second instance of the same gap exists on another project, so the bar in "A
  rule needs a second instance" is met. The blocker above carries it. The
  order of 2026-09-08 is for a round taking R3.1 and the four notes, and
  names no rule; whether a rule is written, and in what words, is the
  maintainer's to direct, so nothing is written for it here.

**Round 4's independent verification, recorded before its findings.** The
reviewer reproduced every figure this description states from its own command
rather than accepting it, and reports every one of them correct. `git diff
--numstat 60f39fb..53125cb -- docs/tier-review-model.md docs/adr` returns 209
and 0 on `docs/tier-review-model.md`, 341 and 0 on the new ADR-0004 and 35 and
0 on ADR-0002, which sum to the 585 insertions and 0 deletions step 1 of How
to verify derives. `git diff --numstat 49b5c00..53125cb --
docs/tier-review-model.md` returns 176 and 38, and `git diff --numstat
8cf72a3..53125cb -- docs/tier-review-model.md` returns 130 and 56. `git diff
--numstat d867af9..53125cb -- docs/tier-review-model.md docs/adr` returns 48
and 23 on the model and 44 and 12 on ADR-0004. `grep -c "^## "
docs/tier-review-model.md` returns 9 at 60f39fb and 9 at 53125cb, against the
nine rows of the document's index. `git show
<commit>:docs/ai-contributor-policy.md | md5sum` returns the identical
`c98a10b7` at both commits, so the map is correctly untouched. `git ls-tree
--name-only <commit> docs/adr/ | wc -l` returns 3 at 60f39fb and 4 at 53125cb,
with three annotations on ADR-0002 against two. `grep -l "^tier: trivial"
docs/tickets/done/*.md | wc -l` returns 7, `grep -l "^tier: critical"
docs/tickets/done/*.md | wc -l` returns 19 and `ls docs/tickets/done/*.md | wc
-l` returns 29, all at 53125cb, and `grep -rl "closed trivial under the
process-document line" docs/tickets/done/ | wc -l` returns 0. `git log
--oneline 60f39fb..53125cb | wc -l` and `git log --format='%b'
60f39fb..53125cb | grep -c "Co-Authored-By: Claude Opus 5"` return 17 and 17.
The board row, the directory and the frontmatter agree. The reviewer did not
take round 3's sweep on trust either: it ran its own sweep of the whole change
for routes of round 3's class, and worked its own cases against the entry,
which is where R4.2 and R4.6 come from.

**The falsifier discharged on this occasion.** The occasion the **Retired
when:** line names is every independent review of a critical-tier
process-document change, and round 4 is one. `grep -rl "closed trivial under
the process-document line" docs/tickets/done/` returned 0: the population is
empty, and there was nothing to read.

**The class signal fired on R4.3, and the wording matched without strain.**
R3.1 was a first-column finding on the who-may-add paragraph of "The operative
test"; R4.3 is a second-column finding on that same paragraph, lying inside
R3.1's fix. That is the pattern "What a review reports" names, in the order it
names it, and the reviewer records explicitly that this is **not** a fifth
near-miss: the signal's words reached the case as written, with nothing
stretched to make them fit. That is worth recording beside the near-misses of
the signal's wording already on record — four of them, by the reviewer's own
count and not by any command, this ticket's R3.1 and the OMN-022-003 instance
among them — because it is evidence about when the wording holds, where the
record so far is only evidence about when it does not. The repairs-of-repairs
signal in "When review ends" fires as well, and at its widest: 3 of 3 of round
4's must-fixes sit inside round 3's fix.

**The ten-route sweep was short, and the corrected count is thirteen.** The
sweep recorded under **The class round 3 repaired** enumerated ten routes of
the shape *which routes does this change give an executor to change a control
that constrains it?* Round 4 found three the sweep missed. Route 11 is R4.2 —
entry 2's disagreeing-documents clause, which is unbounded and sits in the
diff. Routes 12 and 13 are the two reads R4.5 names, the bold-words read and
the process-document-definition read; both are bounded, and the sweep did not
name them. Of the ten already recorded, routes 1 to 3 and 7 to 10 are
genuinely bounded, routes 4 and 5 hold as the round-3 repair leaves them, and
route **6 does not hold**, which is R4.4: its repair widens the count the
falsifier takes and does not bound the route, because a closure that omits the
marker sentence still leaves the readable population.

Findings of round 4, on 53125cb:

- R4.1 · permits · "The operative test", the who-may-add paragraph, the
  closing gloss added at `53125cb` — "the retirement ticket … where widening an
  entry is an amendment with record" · "Retiring a control" allows amendment
  only where the match is technical and the correction small, requires the
  decision record to say why the match was technical, and makes retirement the
  default; neither of its second-column bullets contemplates widening the
  *entry* at all — the fourth widens the *falsifier*. The gloss therefore
  writes a permission that section does not grant, and writes it in the one
  direction that keeps a lowering entry in the document and makes it wider —
  remedy: name the retirement ticket and let "Retiring a control" choose
  between retirement and amendment, rather than choosing for it; cost of the
  tightening: a ticket that wants to widen an entry must show its match was
  technical, over a population of 0 today — the whole negative list lands in
  this change, 209 insertions and 0 deletions on `docs/tier-review-model.md`
  at 53125cb against 60f39fb from `git diff --numstat 60f39fb..53125cb --
  docs/tier-review-model.md`, so no baseline entry exists to widen, and none
  of the 19 `tier: critical` closures in `docs/tickets/done/` at 53125cb
  carries one; inside previous fix: yes (R3.1's). **Must-fix, deliberately not
  repaired: a fifth round is the maintainer's to order.**
- R4.2 · permits · "The operative test", negative list entry 2, "Where the two
  disagree, containment still passes — every question is still answered in
  full" · contradicted by the same commit's R3.3 repair, which makes the
  **Nothing left** half demand that the untouched document say *everything the
  removed text said, and not merely that it covers the same subject*; a
  document that disagrees does not say what the removed text said. The clause
  states the topic-coverage reading R3.3 excluded, and it resolves the case to
  `trivial` where the test as repaired returns `critical` — so an executor may
  correct alone, at `trivial`, a document that binds it. ADR-0004 carries both
  readings, the clause at L108 and the excluding definition at L217 — remedy:
  the case fails **Nothing left**, so the entry does not apply to it and the
  clause goes; cost: the case pays a round, which is what the bold words
  already return for it; 0 of the 7 `tier: trivial` closures in
  `docs/tickets/done/` at 53125cb are affected, by `grep -l "^tier: trivial"
  docs/tickets/done/*.md | wc -l`, and both worked examples are unaffected;
  inside previous fix: yes (R3.2's). **Must-fix, deliberately not repaired.**
- R4.3 · refuses · "The operative test", the same paragraph, "whatever column
  the finding falls in. It goes to the ticket and the round" · a *first*-column
  must-fix on a baseline entry says the entry is too wide and is therefore
  narrowed, which raises; the sentence routes it to a retirement ticket
  anyway, where "Retiring a control" routes only second-column findings and
  raising is the direction "Separation of duties" gives the executor. Honest
  tightening is made to pay a ticket and a round it does not owe — remedy: bar
  in-round *widening* rather than in-round action, and drop "whatever column";
  cost: none, since the remedy removes a refusal and adds nothing; inside
  previous fix: yes (R3.1's). **Must-fix, deliberately not repaired. The class
  signal fired here — see above.**
- R4.4 · note · route 6 of the sweep under **The class round 3 repaired**, the
  marker sentence · the round-3 repair does not bound the route it was written
  for: a closure that omits the sentence still leaves the *readable*
  population, and only the count the falsifier takes is widened — **note,
  recorded and not repaired**, with the remedy left to whatever round the
  maintainer orders. Inside previous fix: yes (R3.4's).
- R4.5 · note · the sweep itself · it omits two reads of the same shape, the
  bold-words read and the process-document-definition read — **note, recorded
  and not repaired**; both are bounded, and they are routes 12 and 13 of the
  corrected count above. Inside previous fix: yes.
- R4.6 · note · "The operative test", negative list entry 2 · in the
  reviewer's words: *text containment makes a typo-fixing correction fail
  entry 2, so the reader must fall through to entry 3, which is unstated.* The
  entry number is the reviewer's and is transcribed as recorded rather than
  renumbered here; round 3's verification recorded the same gap as an
  interaction between entry 2 and entry 4 left unstated. **Note, recorded and
  not repaired.** Inside previous fix: yes (R3.3's).

After the round, on its own lines:

- **No condition of "When review ends" was met by round 4.** Not condition 1:
  the round found three must-fixes. Not condition 2: none of the three lies
  inside a limit this ticket records, since Out of scope records only the
  operative test's five clauses and what each tier requires, and all three sit
  inside the rule this change writes. Not condition 3: none adds an entry to
  an enumeration maintained against an adversary. The cap stands at three
  rounds, round 4 was ordered rather than taken, and nothing in it is
  repaired, so the ticket blocks to the maintainer again with this record
  attached.
- **The no-block reasoning of round 4 failed, and the failure is round 1's.**
  Round 4 declined to block on the ground that "every repair tightens, and
  tightening is the executor's direction". R4.1 and R4.2 loosen: the first
  writes a permission "Retiring a control" does not grant, in the direction
  that keeps and widens a lowering entry, and the second resolves to `trivial`
  a case the test as repaired returns `critical` for. In the reviewer's words,
  *round 1's failure recurred* — round 1's entire finding on this ticket was
  an executor lowering a tier while believing it had not, and the same thing
  has happened again, this time under an explicit claim to the contrary. The
  claim carried the ordered round to a no-block, and it was wrong on two of
  the three must-fixes the next reviewer returned.
- **The round-table deviation was judged correct.** Round 4 read the choice to
  put 53125cb on round 3's row rather than opening a round-4 row at the block:
  the record asks for "the commit that repaired it", 53125cb repaired round 3,
  and a round-4 row written then would have asserted a count for a review that
  had not run. The derived total was 6 + 2 + 1 = 9 either way at that point,
  three of them inside a previous fix, and each round's reviewed commit is
  readable from its findings heading. Round 4 has a row of its own, written
  after the round returned.
- **The reviewer's verdict on the ordered round: justified.** It repaired a
  real rule defect and exposed three more in the operative test. The cap's own
  **Retired when:** line in "When review ends" retires the cap when a ticket
  blocked at it has its maintainer order a further round that finds a rule
  defect; this case matches that line, and it is recorded so a later reader of
  the falsifier finds the case rather than reconstructing it.
- **Post-review check after round 4 (2026-09-08)**, per
  `docs/quality-gates.md`, "Review isolation", made at a0adb0b before the
  first edit of this record: `git status --porcelain` in this worktree
  returned no output, and `git worktree list` showed twelve worktrees, none
  created by this ticket's executor and none left behind by the review;
  `A:/projects/wt/review-EM-007-002` is the reviewer's own tree, at a0adb0b
  and detached, and this tree was not written to. Nothing untracked, nothing
  modified, so there is no finding against the review to record beside round
  4's row.
