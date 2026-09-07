---
id: EM-007-002
title: A change to a process document is trivial by the operative test and critical by ADR-0002
status: blocked
tier: critical
complexity: S
dependencies: []
claimed_by: claude-opus-5
claimed_at: 2026-09-07
blocked_at: 2026-09-07
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

**BLOCKER (2026-09-07):** the independent review of 49b5c00 reached, in
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
repair and the class are recorded in the Review section below. The ticket is
blocked to the maintainer on one question the repair could not answer
without narrowing the maintainer's own sentence; the `BLOCKER (2026-09-07)`
note in Notes above states it.

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
    list it duplicated, where that list is unchanged." **Kept**, because the
    maintainer's decision requires it: EM-007-001 is exactly this shape and
    is one of the four closures the decision preserves. Removing it would
    contradict the answer given.
13. "Wording that leaves every rule's conditions and every procedure's steps
    as they were." **Kept** — it is the plain content of "does not alter a
    rule or a procedure", and it is what leaves ordinary work `trivial`.
14. How far entry 12 reaches: whether correcting a *restatement* of a rule
    or a procedure, in a document that is not where the question is settled,
    to agree with an unchanged document that is, alters a procedure.
    **Deferred to the maintainer** — the `BLOCKER (2026-09-07)` note above.
    Answering it either narrows the maintainer's sentence or extends a
    carve-out to a closure the maintainer did not have in front of them.

One clause is added by this repair and is itself raising: the two lists are
marked for who may add to which, so that a future executor reads the
asymmetry at the point where it would otherwise widen the exemption.

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
either. Widening a blocked, six-must-fix change by a second document's rule
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
  **A change to a process document** in "The operative test", at 99e7ae7.
  The line is one sentence: `critical` when the change adds, alters or
  retires a rule or a procedure, `trivial` when it does not. What surrounds
  it is what makes the sentence usable without asking — what a process
  document is, the two definitions, the two lists with the note that neither
  is closed and who may add to which, and one closed ticket on each side.
- [x] AC2: the statement and ADR-0002 agree, and the record is annotated
  rather than amended — see the annotation dated 2026-09-07 under
  EM-007-002 at the end of
  `docs/adr/0002-critical-tier-review-in-a-single-maintainer-repository.md`,
  the third annotation on that record, read from `grep -c "^## Annotation"
  docs/adr/0002-*.md` at 99e7ae7 against two at 60f39fb. What agrees is the
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
  population. The population is empty at 99e7ae7: no change has closed under
  a line that lands with this ticket, against the seven closed tickets
  carrying `tier: trivial` in `docs/tickets/done/` at 99e7ae7 that closed
  before it, read from `grep -l "^tier: trivial" docs/tickets/done/*.md |
  wc -l`.
- [ ] AC4: **blocked.** The four closures the decision names — EM-007-001,
  EM-010-002, EM-012-001-001 and the entries of the batch EM-017 — stand,
  and the record does nothing to them; reclassifying them was a consequence
  of answer 1, which was not chosen. Each recorded the reading in its own
  Notes before it was written down, checked by reading all four at claim.
  Round 1 found a fifth ticket the criterion reaches and the maintainer's
  carve-out does not name: **EM-018-001** rewrote `templates/TICKET.md`'s "How to use
  this template" steps — 12 insertions and 7 deletions there, plus one line
  added to `.gitignore`, read from `git show --numstat 5750d73` — and closed
  `standard`, self-merged, with no independent review. Whether that is a
  closure at a tier the decision contradicts turns on the question in the
  `BLOCKER (2026-09-07)` note, and the record does nothing to it until that
  is answered. Note also that the repair of R1.1 means the EM-010-002 shape
  — an annotation that changes how a decision is read — costs a round from
  here on; the closure itself stands, since the decision governs closures
  from 2026-09-07 forward.
- [ ] AC5: round 1 has run and is recorded below with its six must-fixes and
  three notes. A round 2 has not run, and the ticket is blocked before it.

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
  read the falsifier and do nothing.
- AC4 — a maintainer reading the record sees why four closures stand, sees
  the fifth the decision did not consider, and is asked rather than told.
- AC5 — a reviewer of round 2 reads round 1's nine finding lines and the
  class beside them, and can test whether the repair was at the class or at
  the instances.

Round 1's six must-fixes are repaired at the class stated above, in the
form the contributor policy's §6 asks for: the class question, the siblings
it enumerates, and what a reader does differently for each, since the change
has no suite. R1.4, R1.5 and R1.7 fall outside that class and are repaired
as instances, in those words — R1.4 by naming EM-018-001 and blocking on
what the record does about it, R1.5 by routing to EM-007-002-002 with the
scope judgement stated, R1.7 by giving the falsifier an occasion.

### Out of scope (per ticket)
Confirm nothing here exceeds the ticket's scope:
- The operative test's five clauses are unchanged. `git diff --numstat
  60f39fb..HEAD -- docs/tier-review-model.md` gives 99 insertions and 0
  deletions at 99e7ae7 against 60f39fb, the commit this branch was created
  from, so no line of the document that existed before this branch was
  altered; the round-1 repair rewrote only lines this branch had added,
  which `git diff --numstat 49b5c00..HEAD -- docs/tier-review-model.md`
  shows as 54 insertions and 26 deletions.
- What each tier requires is unchanged. "The tiers" is untouched by the same
  diff, and the annotation on ADR-0002 leaves the Decision as it stands. The
  occasion added to the falsifier under R1.7 is read against this limit and
  stays inside it: it says when this rule's own falsifier is checked, which
  "Retiring a control" requires of every falsifier — "stated so that a
  reviewer could recognise it" — and it binds a reviewer already reading
  this paragraph, because this paragraph is what made the change under
  review `critical`. It adds nothing to what `critical` requires of a change
  outside this rule.
- Tempting and deferred: the one-line summary at the foot of the section
  carries clauses 1 to 4 and not clause 5, so a contributor who reads only
  the summary gets `trivial` for a rule change. That is a defect this change
  makes more visible and does not create. It is raised as EM-007-002-001
  under §4 rather than fixed here. `docs/adr-process.md`'s wider sentence is
  raised the same way as EM-007-002-002, for the reasons stated above.

### How to verify
1. `git diff --numstat 60f39fb..HEAD -- docs/tier-review-model.md docs/adr`
   — three files at 99e7ae7 against 60f39fb: 99 and 0 on
   `docs/tier-review-model.md`, 35 and 0 on ADR-0002, 142 and 0 on the new
   ADR-0004. 276 insertions and 0 deletions in total, derived from those
   three rows.
2. Read the whole of "The operative test" in `docs/tier-review-model.md` as
   it stands, not the diff — the reading "When review ends" asks for before
   a repair is handed back, done before this description was written. Three
   defects were found by that reading and fixed in the same commit: the
   decision-record entry still said a record was "not a process document",
   which contradicts the definition above it now that map-named documents
   are in the class; the falsifier named "this section's parent" where it
   meant "Retiring a control"; and the falsifier did not say why a reviewer
   would have this paragraph open on the occasion it names.
3. `grep -c "^## " docs/tier-review-model.md` — 9 at 60f39fb and 9 at
   99e7ae7, against the nine rows of the document's index, so no section was
   added, removed or renamed.
4. `git show 60f39fb:docs/ai-contributor-policy.md | md5sum` against the
   same command at 99e7ae7 — identical, `c98a10b7`, so the map is untouched.
5. `git ls-tree --name-only <commit> docs/adr/ | wc -l` — 3 at 60f39fb and 4
   at 99e7ae7. ADR-0004 carries `status: proposed`; `templates/ADR.md` step
   3 and ADR-0003's own line move it to `accepted` at the closing commit,
   which has not been made.
6. Check the four closures the decision leaves standing: `grep -n -i "rule
   or a procedure" docs/tickets/done/*.md`.
7. `git log --format='%s%n%b' 60f39fb..HEAD` — four commits at 99e7ae7,
   each ending in the co-authorship trailer; the commits after it carry this
   description and the block, and end in it too.

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
- Cost of the round-1 repair, measured at 99e7ae7: the EM-010-002 shape
  costs a round from here on, which is 1 of the 7 tickets carrying `tier:
  trivial` in `docs/tickets/done/`, read from `grep -l "^tier: trivial"
  docs/tickets/done/*.md | wc -l`; and every independent review of a
  critical-tier process-document change carries one extra read, against 19
  of the 29 closed tickets in `docs/tickets/done/` carrying `tier: critical`
  at 99e7ae7, read from `grep -l "^tier: critical" docs/tickets/done/*.md |
  wc -l` and `ls docs/tickets/done/*.md | wc -l`. The population that read
  covers is empty at 99e7ae7.

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
| 2 | — | — | — | Round 2 pending |

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

Round 2 pending.
