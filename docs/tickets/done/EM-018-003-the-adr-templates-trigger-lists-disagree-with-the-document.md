---
id: EM-018-003
title: The ADR template's trigger lists disagree with the document in both directions
status: done
tier: standard
kind: defect
impact: degraded
delivery: maintenance
why: "Without aligning them, the template tells a contributor to write a record where the document says none is owed, and stays silent where the document says the record is the control."
complexity: S
dependencies: [EM-018-002]
claimed_by: claude-opus-5
claimed_at: 2026-09-15
closed_at: 2026-09-15
blocked_at:
closed_at:
---

# EM-018-003 — The ADR template's trigger lists disagree with the document

## Why this ticket should be worked

The affected outcome is whether a contributor using the template writes the
records the process asks for and no others.

EM-018-002 replaced the template's closing test with a pointer to
`docs/adr-process.md`, "When to write one". The two bullet lists above that
sentence were outside its Files and remain. They are a second statement of the
trigger list the document states in full, carrying no falsifier and referencing
nothing, and they diverge from the document in both directions at once.

**Wider than the document.** The template's fifth write-one bullet reads "A
workflow rule in `docs/ai-contributor-policy.md`, `docs/ticket-lifecycle.md`
or `docs/tier-review-model.md` changes" — so a contributor whose change
matches it writes a record. The document says the trigger "does not reach a
rule added inside a document, or extended in place one rule at a time, under
an existing decision", and works seven such rules explicitly as owing none —
EM-008, EM-009, EM-010, EM-012, EM-016, EM-019-001 and EM-021's
second-instance bar. A reader whose change matches the bullet exactly is not
"in doubt" and never reaches the pointer. So the wider reading that
EM-019-001-001-001 removed from the document, and that EM-018-002 removed from
the template's closing sentence, survives one list item above it.

**Narrower than the document.** The same list omits the retirement clause
entirely. The document's trigger reaches "a rule retired or amended under
`docs/tier-review-model.md`, 'Retiring a control'", and the test carries a
carve-out saying that record is owed however the rule arrived, because there
the record *is* the control: the retired text leaves the document and survives
nowhere else. No template bullet matches it. The list is also narrower on four
items — "A library" for "A dependency", "public engine API" for "public API",
"a locked decision in the adopting project's own DESIGN.md" for "a previously
locked design decision", and three named documents for "a workflow rule".

Deferring this leaves the repository stating one trigger list two ways that
disagree, in the file a contributor copies, on the case the correction was
about. It is `degraded` rather than blocking because the pointer beneath the
lists reaches the correct test for anyone who is in doubt.

## Context

Raised by the one independent review pass on EM-018-002 (findings R1.1, R1.2
and R1.3), which recorded them and routed them: that ticket's Files names only
"the closing sentence of 'When to write an ADR vs not'", so the lists lie
inside a limit it records, and under the second condition of "When review
ends" the findings go to a ticket that owns them, raised because none existed.

## Specification

Documentation change only.

### Files

- `templates/ADR.md`, the two bullet lists under "When to write an ADR vs
  not".

### Public surface

The template is copied by adopters. Its statement of when a record is owed is
an instruction they follow.

### Behaviour

- The template does not carry a second full statement of the trigger list that
  `docs/adr-process.md` states in full, per "Retiring a control": "A rule
  stated in two documents carries one falsifier, stated where the rule is
  stated in full and referenced from the other."
- Whichever form is chosen — replacing the lists with the pointer, or
  restating them faithfully with a reference — the template and the document
  give the same answer for a rule added under an existing decision, and for a
  rule retired or amended under "Retiring a control".
- The adopter's case is considered: the template is copied into projects that
  may not hold `docs/adr-process.md`. If the lists go, the description says
  what an adopter who copies only `templates/` is expected to do, as EM-018
  already had to for the documents it cites.

## Acceptance criteria

1. AC1: worked through the template alone, a rule added inside a document
   under an existing decision returns the same answer as
   `docs/adr-process.md` gives it — no record — and EM-021's second-instance
   bar is the worked case.
2. AC2: worked through the template alone, a rule retired or amended under
   "Retiring a control" returns a record owed.
3. AC3: the template carries no second full statement of the trigger list, or
   carries one that references the document and matches it item for item.
4. AC4: `docs/adr-process.md` is unchanged.
5. AC5: a change to a process document is `standard` on one independent
   review pass, per "The operative test"; the pass is recorded as one row of
   the Review table.

## Out of scope

- `docs/adr-process.md`, which EM-019-001-001-001 settled.
- The closing sentence, which EM-018-002 settled.
- Any other section of `templates/ADR.md`.

## References

- `templates/ADR.md`, "When to write an ADR vs not".
- `docs/adr-process.md`, "When to write one" — the list and the test in full.
- EM-018-002, Review, R1.1, R1.2 and R1.3 — the findings routed here.
- EM-019-001-001-001 — the correction to the document's test.
- `docs/tier-review-model.md`, "Retiring a control" — the one-statement rule
  and the retirement carve-out.

## Notes

The id was read with the next-id command as EM-023 corrected it: `git log
--full-history --diff-filter=AR --name-only --format= -- docs/tickets`, with
the EM-018 children extracted, returns `EM-018-001` and `EM-018-002`.

## PR Description

### Ticket
EM-018-003 — The ADR template's trigger lists disagree with the document in
both directions.

### Tier
`standard`, on one independent review pass. `templates/ADR.md` states a
procedure a contributor performs and sits under `templates/`, which "The
operative test" names as a process document. The pass ran against d530cc6 and
is row 1 of the Review table.

### Summary
The template's two bullet lists were a second statement of what
`docs/adr-process.md` states in full, carrying no falsifier and referencing
nothing, and diverging in both directions: wider, because the workflow bullet
fired on any rule change in three named documents including every rule added
under a decision already taken; narrower, because no bullet matched a rule
retired or amended under "Retiring a control". The lists now quote the
document item for item, under a line naming it as the full statement and the
governing text.

### Acceptance criteria
- [x] AC1: worked through the template alone, a rule added inside a document
  under an existing decision returns the same answer the document gives it,
  and EM-021's second-instance bar is the worked case. EM-021's bar is one
  paragraph added to `docs/tier-review-model.md` under ADR-0003's decision
  that a rule is held to evidence. Template alone: the workflow-rule trigger
  fires on "a workflow rule changes", and the clause beneath the lists then
  says that trigger "does not reach a rule added inside a document, or
  extended in place one rule at a time, under an existing decision: the
  constraint is that decision's, and that decision has its record" → **no
  record**. The document places EM-021's bar "on the second side", among the
  rules that "produced no record, and under this line none was owed". Same
  answer, and reached by the same clause rather than by a conclusion the
  reader must already hold — which is what the round-1 reviewer found the
  first attempt could not do.
- [x] AC2: worked through the template alone, a rule retired or amended under
  "Retiring a control" returns a record owed. The workflow-rule bullet reads
  "including a rule retired or amended under `docs/tier-review-model.md`,
  'Retiring a control'", quoted from the document, and the non-reach clause
  beneath does not exempt it → **record owed**, with what that record carries
  stated in the same bullet.
- [x] AC3: the template carries a statement that references the document and
  matches it item for item — AC3's second limb. `diff` of the two lists,
  taking the bullet lines from `docs/adr-process.md` and from
  `templates/ADR.md`, returns a single difference: "A previously locked design
  decision is revised" gains "— in an adopting project, one recorded in its
  own DESIGN.md". That is the adopter idiom EM-018 settled for this template,
  which names "the adopting project's own DESIGN.md" in two other places, and
  it adds no item and removes none. Every other bullet, including the
  retirement clause and all four non-triggers, is verbatim.

  The reference above the lists says the document "states this rule in full and
  carries its falsifier … where the two differ, that document governs", which
  is the form "Retiring a control" asks for: the rule stated in full in one
  place with its falsifier, and referenced from the other.
- [x] AC4: `docs/adr-process.md` is unchanged. `git diff main...HEAD
  --name-only`, run after ec4c6be, names `templates/ADR.md`, this ticket file
  and the board row, and nothing under `docs/adr/` or `docs/adr-process.md`.
- [x] AC5: one independent review pass, run against d530cc6 by an agent that
  did not perform the work and did not receive the executor's reasoning,
  recorded as row 1 of the Review table below. It returned six must-fixes over
  eight findings, all repaired at ec4c6be.

### Falsification
N/A for a behavioural claim — this repository publishes documents and runs no
suite. Per criterion, what a reader does differently: a contributor deciding
whether their change needs a decision record reads the same triggers and the
same exclusions in the template as in the document, including the two the old
lists got wrong, and is told which text governs if the two ever drift.

For the must-fixes repaired, per the contributor policy's §6:

- R1.4, R1.5, R1.6, R1.7 — class: **what can a reader holding only this
  template actually decide?** The deleted lists are the instance. The question
  was asked of every case the section is meant to settle. Siblings, each
  checked:
  - **The four triggers and four non-triggers** — the instance. Gone in the
    first attempt, so an adopter could not answer a dependency swap, an API
    shape change, a top-level package or a rename — the cases they will
    usually have. Repaired: quoted, item for item, with the document named as
    governing.
  - **The non-reach clause** — the sharper defect, reported as R1.5. The
    first attempt's summary dropped "or extended in place one rule at a time"
    while bolding "amended", so a contributor extending a rule's sentence in
    place found the trigger fitting and the exclusion not, and would have
    written a record the document refuses. That clause was added to the
    document by a review round of EM-019-001-001 for exactly that
    misplacement. Repaired: quoted whole.
  - **The one positive trigger's definition** — reported as R1.6. It is
    defined in `docs/tier-review-model.md`, which the adopter sentence did not
    name, so an adopter following that sentence took one document and still
    could not work the trigger. Repaired: both documents named.
  - **The section heading** — reported as R1.7. "When to write an ADR vs not"
    named a decision procedure over a section that stated no "when" and one
    "not". Repaired by restoring the content rather than renaming the heading,
    which would have changed the section list EM-018's AC4 fixed.
  - **The closing "when in doubt" sentence** — checked; it is about the test,
    not the lists, and is unaffected by their return. See R1.1.
  What a reader does differently: an adopter holding only `templates/` decides
  the ordinary cases in place, and is told which document governs the ones it
  does not settle.
- R1.1 — class: **which text outside this ticket's Files did the change
  touch?** The closing sentence is the instance, and the only one. This
  ticket's Files names "the two bullet lists under 'When to write an ADR vs
  not'" and its Out of scope reserves "the closing sentence, which EM-018-002
  settled"; the first attempt deleted and rewrote it. Asked of the rest of the
  file: `git diff main...HEAD -- templates/ADR.md` touches no other section,
  and the rest of the template is byte-identical. Repaired: EM-018-002's
  sentence is restored verbatim.
  What a reader does differently: a reader following EM-018-002's record to
  the sentence it landed finds that sentence, not a replacement made under a
  later ticket that did not own it.
- R1.2 — class: **which sentences assert what another document contains?**
  The reference's first sentence is the instance: it listed a four-item
  inventory of the target, which is the drift-prone form EM-018-002's own R1.5
  had just repaired in the sentence that repair produced. Siblings checked:
  the restored closing sentence names the section and the rule it acts under
  and asserts nothing about contents; the new reference now says the document
  states the rule in full, carries its falsifier and governs on a difference —
  three claims about its status, none about its contents.
  What a reader does differently: the reference survives a restructuring of
  `docs/adr-process.md` that would have falsified an inventory of its parts.
- R1.3 — class: **which citations claim a source says something it does not?**
  The adopter sentence is the instance: it asserted that the README's "Start
  here" table directs an adopting project to take `docs/adr-process.md` with
  the template. That table is a six-row reading map of this repository and
  directs no such thing, and an adopter's README is their own. Siblings
  checked: every other file this template cites is either named as the
  adopting project's own, which is EM-018's settled form, or is a document of
  this repository named as such. Repaired: the template says in its own voice
  which documents it is written against.
  What a reader does differently: an adopter is told what to do by the
  template rather than referred to a table that does not say it.

### Out of scope (per ticket)
Confirmed as it now stands, and one breach in the first attempt is recorded
rather than smoothed.
- `docs/adr-process.md` — untouched throughout.
- **The closing sentence EM-018-002 settled** — the first attempt, at d530cc6,
  deleted and rewrote it, which exceeded this limit. The round-1 reviewer
  caught it and it is restored verbatim at ec4c6be. The breach is recorded
  here because a closed ticket's repair was overwritten by a later ticket that
  did not own it, and that is worth a reader seeing rather than a diff that
  ends up clean.
- Any other section of `templates/ADR.md` — untouched.

### How to verify
1. `sed -n '/^## When to write an ADR vs not/,$p' templates/ADR.md` — the
   section as it stands.
2. `diff <(sed -n '/^Write an ADR when:/,/^- Configuration any contributor would make\./p' docs/adr-process.md | grep '^- ') <(sed -n '/^Write one when:/,/^- Configuration any contributor would make\./p' templates/ADR.md | grep '^- ')`
   — one difference, the DESIGN.md adaptation, which is AC3.
3. `grep -c 'extended in place one rule at a time' templates/ADR.md` — 1,
   which is R1.5.
4. `git diff main...HEAD --name-only` — no document under `docs/`, which is
   AC4.

### Risks / follow-ups
- **The template now carries a faithful copy, which is a maintenance cost the
  criterion names.** A change to the document's list touches two files. AC3's
  second limb accepts that in exchange for a template an adopter can use, and
  the reference says the document governs on a difference, so a drift is a
  defect in the copy rather than an open question. `docs/adr-process.md`
  carries a **Retired when:** aimed at the very line the template's non-reach
  clause quotes; if that falsifier fires, this copy is one of the two sites
  that must move, and whoever moves the document should search `templates/`.
- **A closed ticket's repair was overwritten and restored.** EM-018-002
  settled one sentence; this ticket's first attempt replaced it. Nothing in
  the tree goes red when a later ticket edits text a closed ticket owns — the
  Out-of-scope line caught it only because a reviewer read it. That is one
  instance; "A rule needs a second instance" bars writing a rule on one, so it
  is recorded here rather than raised.

### Review
One independent review pass, per "The operative test" for a change to a
process document. No second pass is taken.

| Round | Must-fix | Where (rules / lists / documents / tests) | Inside previous round's fix | Repaired by |
|---|---|---|---|---|
| 1 | 6 (of 8 findings) | documents: the section stated no trigger and no non-trigger a reader could apply, leaving an adopter holding `templates/` unable to answer the ordinary cases (must-fix, second column); the two-case summary dropped "or extended in place one rule at a time" while bolding "amended", so an in-place amendment matched the trigger and not the exclusion (must-fix, second column); the closing sentence EM-018-002 settled was deleted and rewritten, which this ticket's Out of scope reserves (must-fix); the reference asserted a four-item inventory of the target, the defect EM-018-002's R1.5 had just repaired (must-fix); the adopter sentence cited the README's "Start here" table for a direction it does not give (must-fix); the one positive trigger is defined in a document the adopter sentence did not name (must-fix, second column); the heading named a decision procedure over a section that stated none; the section's only imperative was addressed to an adopting project rather than to the contributor deciding | — | ec4c6be |

Derived from the row and not asserted beside it: six must-fixes over one
review round, all repaired. Round 1 has no round before it, so its
inside-previous-fix cell reads `—` and no line is uncountable. Three of the
six sat inside a fix a *closed* ticket had made — EM-018-002's — which the
round table's inside-previous-fix field does not reach, since that field asks
about the previous round of this review; it is recorded here instead.

- R1.4 · refuses · must-fix · `docs/adr-process.md`, "When to write one", the four triggers and four non-triggers; the ticket's Public surface, "The template is copied by adopters. Its statement of when a record is owed is an instruction they follow" · the section stated no trigger and no non-trigger a reader could apply, so an adopter holding only `templates/` could not answer a dependency swap, an API shape change, a top-level package or a rename, and the two cases kept were conclusions with no test between them — remedy: keep the reference as the full statement and set the document's lists beneath it, quoted, with a line saying the document governs on a difference, which AC3's second limb permits; cost, if the remedy tightens a control: none — it adds no refusal and restores text an adopter could already read; the maintenance cost is that the document's list now touches two files; inside previous fix: —
- R1.5 · refuses · must-fix · `docs/adr-process.md`, "It does not reach a rule added inside a document, **or extended in place one rule at a time**, under an existing decision" · the summary dropped that clause while bolding "amended", so a contributor extending a rule's sentence in place found the trigger fitting and the exclusion not, and would write a record the document refuses — remedy: quote the clause whole; cost, if the remedy tightens a control: none — the remedy removes a demand for a record; inside previous fix: —
- R1.1 · permits · must-fix · the ticket's Out of scope, "The closing sentence, which EM-018-002 settled" · the change deleted and rewrote that sentence, exceeding the limit its own ticket records, on a line a closed ticket owns — remedy: restore it verbatim and confine the edit to the lists; cost: none; inside previous fix: —
- R1.2 · permits · must-fix · EM-018-002, R1.5 — a pointer "asserts nothing about the target's contents, which is the property a pointer is chosen for" · the replacement asserted a four-item inventory of the target, reinstating the defect that repair had just fixed, in the sentence it produced — remedy: name the section and the rule it acts under and assert nothing about its contents; cost: none; inside previous fix: —
- R1.3 · permits · must-fix · `README.md`, "Start here" · the adopter sentence asserted that table directs an adopting project to take `docs/adr-process.md` with the template; it is a reading map of this repository and directs no such thing, and the adopter's README is their own — remedy: state the expectation in the template's own voice and drop the attribution; cost: none; inside previous fix: —
- R1.6 · refuses · must-fix · AC2, worked "through the template alone" · the one case where the template says a record is owed is defined in `docs/tier-review-model.md`, which the adopter sentence did not name, so an adopter following it took one document and still could not work the trigger — remedy: name both documents; cost: none; inside previous fix: —
- R1.7 · refuses · note · the heading "When to write an ADR vs not", and EM-018 AC4, "No template's structure or section list changes" · the heading named a decision procedure over a section stating no "when" and one "not" — remedy: restore the content rather than rename the heading; cost: none; inside previous fix: —
- R1.8 · refuses · note · the deleted "When in doubt, apply the test …" · the replacement described what another document contains but never told the contributor to apply it, leaving the section's only imperative addressed to an adopting project — remedy: restore the directive with R1.1; cost: none; inside previous fix: —

Five of the eight findings are second-column, and they are the ones that
changed the work. The first attempt read as a tidy repair — a divergent copy
replaced by a reference — and what it actually did was take a usable
instruction away from the reader the template exists for, while leaving a
two-case summary that was itself wrong on one of the two. That is the failure
"What a review reports" names from the other side: not a review that only
tightens, but a repair that only deletes.

### Definition of Done (all tiers)
The four machine checks do not apply to a repository that publishes documents
and runs no suite; the falsification gate is discharged above, with N/A for
the behavioural claim and a class line per must-fix repaired. Every measured
figure names its baseline in the same sentence and is read from the command
named beside it. The independent pass a process-document change takes has run
and is recorded.
