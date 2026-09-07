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

## PR Description

### Ticket
EM-007-002 — A change to a process document is trivial by the operative test
and critical by ADR-0002

### Tier
`critical` — a rule enters `docs/tier-review-model.md` and a decision record
is annotated. That is process surface under the operative test's fifth
clause and under ADR-0002, and it is `critical` under the very line this
ticket writes down: a rule is added to a process document. Independent
review per ADR-0002 is available in that record's sense and is pending
below.

### Summary
The question this ticket carried was reserved to the maintainer under the
contributor policy's §3 and was answered on 2026-09-07 with the second of
the three answers the Specification set out. `docs/tier-review-model.md`,
"The operative test", now carries the line: a change to a process document
is `critical` when it adds, alters or retires a rule or a procedure, and
`trivial` when it does not. The paragraph says what a rule is and what a
procedure is, what the words do not reach, that neither list is closed,
names EM-012-001 on the `critical` side and EM-007-001 on the `trivial`
side, states the cost the maintainer accepted and the two things that hold
it, and carries its own **Retired when:**. ADR-0002 gains a dated annotation
in the form the repository already uses; nothing above its horizontal rule
changes and its status stays `accepted`.

**Whether a decision record is owed: no.** `docs/adr-process.md`, "When to
write one", as EM-019-001-001 left it, puts a record on the first side of
its line when a decision changes how the process itself is governed — the
form every rule takes, who may review or approve, whether the process
applies to the repository at all — or when a rule is retired or amended
under "Retiring a control", where the record is the only place the retired
text and the matching finding survive. This change is on the second side. It
adds one rule inside one section of one document, under the decision that
put the section there: ADR-0001 adopts the tier model here, and ADR-0002
decides what critical review requires. It changes what the process asks at
one step — which tier one class of change is — and it rewrites no other
rule. Nothing leaves any document: ADR-0002's original text is untouched and
the annotation sits beside it, so the reason the "Retiring a control" limb
exists does not apply. And the practice is already the repository's own, on
this very record: EM-010-002 annotated ADR-0002 where two of its sentences
had grown narrower than the model, and produced no record; EM-012-001 added
to this same paragraph the sentence separating `trivial` from `standard`,
and produced no record. `docs/adr/` holds three records at 60f39fb and three
at a41250f, read from `git ls-tree --name-only <commit> docs/adr/ | wc -l`.
The ticket's own Specification, written before EM-019-001-001 landed that
line, said a record was owed "since it is a workflow rule changing"; the
line drawn since decides otherwise, and this paragraph is the reasoning that
a reader may check against it.

**Second-instance bar.** This ticket was raised at fc9f592 and EM-021 closed
at 3578199, with fc9f592 an ancestor of 3578199 — read from `git merge-base
--is-ancestor fc9f592 3578199` — so the bar in `docs/tier-review-model.md`,
"A rule needs a second instance", does not bind it. Its Context names two
instances regardless: the independent review of EM-007 (finding 12 of round
2) and the independent review of EM-012-001 (finding R2.2 of round 2), each
finding the same conflict on this repository, both readable in
`docs/tickets/done/`.

### Acceptance criteria
- [x] AC1: `docs/tier-review-model.md` states when a change to a process
  document is `critical` and when it is `trivial` — the paragraph beginning
  **A change to a process document** in "The operative test", at a41250f.
  The line is one sentence: `critical` when the change adds, alters or
  retires a rule or a procedure, `trivial` when it does not. The paragraph
  beneath it is what makes the sentence usable without asking — the two
  definitions, the two lists with the note that neither is closed, and one
  closed ticket on each side.
- [x] AC2: the statement and ADR-0002 agree, and the record is annotated
  rather than amended — see the annotation dated 2026-09-07 under
  EM-007-002 at the end of
  `docs/adr/0002-critical-tier-review-in-a-single-maintainer-repository.md`,
  the third annotation on that record, read from `grep -c "^## Annotation"
  docs/adr/0002-*.md` at a41250f against two at 60f39fb. What agrees is the
  Decision, which is untouched and says nothing about which changes are
  `critical`. What was wider than the practice is one Context sentence, and
  the annotation records its narrowed reach, what stands, and the reasoning.
  The amendment-with-record path of "Retiring a control" was not used: that
  path governs a second-column review finding matching a rule's stated
  falsifier, and this is a maintainer's answer to a reserved question, with
  no rule text leaving any document.
- [x] AC3: the rule carries a **Retired when:** line — the one immediately
  beneath the paragraph, naming the evidence (a change closed `trivial`
  under the line, found to have added, altered or retired a rule or a
  procedure after all, more than once), the population (the closed tickets
  carrying `tier: trivial` in `docs/tickets/done/`, of which there are seven
  at a41250f, read from `grep -l "^tier: trivial" docs/tickets/done/*.md |
  wc -l`), how they are read (a maintainer's spot-check of self-merged
  work), and what the rule retires in favour of (ADR-0002's Context read as
  written).
- [x] AC4: no ticket is closed at a tier the decision contradicts. The four
  closed on the narrow reading — EM-007-001, EM-010-002, EM-012-001-001 and
  the entries of the batch EM-017 — are named in the maintainer's decision
  in Notes above and in ADR-0002's annotation, and the record does nothing
  to them: they stand. Reclassifying them was a consequence of answer 1,
  which was not chosen. Each recorded the reading in its own Notes before it
  was written down, which was checked at claim by reading all four:
  EM-007-001 ("ADR-0002's sentence ... is read as applying to changes that
  alter a rule or a procedure; this one alters neither"), EM-010-002 ("no
  rule or procedure changes; a record is annotated"), EM-012-001-001 ("one
  clause completed; no procedure changes") and EM-017 ("No rule or procedure
  changes").
- [ ] AC5: pending — an independent agent has not yet reviewed this. The
  Review section below carries the placeholder row.

### Falsification
N/A — a documentation change with no suite. Per acceptance criterion, what a
reader does differently:
- AC1 — a contributor whose change touches a document under `docs/` or
  `templates/` reads the paragraph and answers the tier question without
  asking anyone, where before the model returned `trivial` for the change
  and ADR-0002 returned `critical` and nothing said which governed. A
  contributor correcting a wrong filename in the lifecycle self-merges it or
  batches it; a contributor adding a rule, changing a threshold, or moving
  where a question is settled summons an independent reviewer. A contributor
  writing or changing a decision record does the same, which the third
  bullet says so that the annotation path is not read as licence.
- AC2 — a reader of ADR-0002 who reaches the Context sentence now reaches
  the annotation with it, and does not conclude that a typo fix in
  `docs/ticket-lifecycle.md` needs an independent review. A reader auditing
  the four `trivial` closures against that sentence finds them answered
  rather than unexplained, and raises no ticket to reclassify them.
- AC3 — a reviewer who finds a change closed `trivial` under this line that
  did alter a rule or a procedure has a falsifier to match the finding to
  and a named population to count it in, and the second such finding retires
  the line in favour of ADR-0002's Context read as written, rather than the
  question being argued again case by case.
- AC4 — a maintainer reading the record sees why four closures stand, and a
  future executor citing them as precedent can see that the precedent was
  checked rather than assumed.
- AC5 — pending.

No review findings are repaired in this description, so the class obligation
of the contributor policy's §6 has nothing to record yet; round 1 has not
run.

### Out of scope (per ticket)
Confirm nothing here exceeds the ticket's scope:
- The operative test's five clauses are unchanged. `git diff 60f39fb..HEAD
  -- docs/tier-review-model.md` shows 71 insertions and 0 deletions in that
  document, so no existing line of the section was altered; the new
  paragraph applies clause 5 to a class of change and does not reword it.
- What each tier requires is unchanged. "The tiers" is untouched by the same
  diff, and the annotation on ADR-0002 leaves the Decision as it stands.
- Tempting and deferred: the one-line summary at the foot of the section
  carries clauses 1 to 4 and not clause 5, so a contributor who reads only
  the summary gets `trivial` for a rule change. That is a defect this change
  makes more visible and does not create. It is raised as EM-007-002-001
  under the contributor policy's §4 rather than fixed here.

### How to verify
1. `git diff 60f39fb..HEAD -- docs/tier-review-model.md docs/adr` — 105
   insertions and 0 deletions across two files, 71 and 34, read from `git
   diff --numstat 60f39fb..HEAD -- docs/tier-review-model.md docs/adr` at
   a41250f against 60f39fb, the commit this branch was created from.
2. Read the whole of "The operative test" in `docs/tier-review-model.md` as
   it stands, not the diff — the reading "When review ends" asks for, done
   before this description was written.
3. `grep -c "^## " docs/tier-review-model.md` — 9 at 60f39fb and 9 at
   a41250f, against the nine rows of the document's index, so no section was
   added, removed or renamed.
4. `git show 60f39fb:docs/ai-contributor-policy.md | md5sum` against the
   same command at a41250f — identical, so the map is untouched.
5. Check the four closures the decision leaves standing: `grep -n -i "rule
   or a procedure" docs/tickets/done/*.md`.
6. `git log --format='%s%n%b' 60f39fb..HEAD` — three commits, each ending in
   the co-authorship trailer.

### Risks / follow-ups
- **EM-007-002-001** raised in `docs/tickets/ready/`, proposed `critical`:
  the section's one-line summary omits clause 5.
- The map in `docs/ai-contributor-policy.md` and the index in
  `docs/tier-review-model.md` needed no update, and neither was touched. No
  section was added, removed or renamed — one paragraph joins "The operative
  test" — and no question moved: the model already settled "What tier is my
  change", and it settles it still. What changed is the answer that section
  gives for one class of change, which the map's rows do not name.
- The line's known weakness is stated in the document rather than here: the
  executor draws it at the moment the executor would prefer `trivial`. The
  falsifier counts exactly that failure, and the population it counts over
  is small — seven closed `trivial` tickets at a41250f, by the command in
  AC3 — so the first two miscounted closures are what retires the line.
- The `trivial` row of "The tiers" and the batch rule in
  `docs/ticket-lifecycle.md` both describe `trivial` work in their own
  words. Neither was edited, and neither contradicts the new line; a
  reviewer finding that one of them now reads wider than the paragraph has
  a finding, and it would be repaired in the round.

### Review
Round 1 pending.

| Round | Must-fix | Where (rules / lists / documents / tests) | Inside previous round's fix | Repaired by |
|---|---|---|---|---|
| 1 | — | — | — | — |
