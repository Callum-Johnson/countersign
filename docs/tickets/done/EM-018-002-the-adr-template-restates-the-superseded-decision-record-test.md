---
id: EM-018-002
title: The ADR template restates the decision-record test in its superseded form
status: done
tier: standard
kind: defect
impact: degraded
delivery: maintenance
why: "Without correcting it, the repository states one test two ways that disagree, and the template carries the wider reading that EM-019-001-001-001 removed from the document it restates."
complexity: S
dependencies: [EM-019-001-001-001]
claimed_by: claude-opus-5
claimed_at: 2026-09-15
closed_at: 2026-09-15
blocked_at:
closed_at:
---

# EM-018-002 — The ADR template restates the superseded decision-record test

## Why this ticket should be worked

The affected outcome is whether a contributor asking "does this need a
decision record?" gets one answer.

`docs/adr-process.md` carried a test whose literal reading reached every rule
added under an existing decision, while the paragraph beneath it said such a
rule owes no record. EM-019-001-001-001 rewrote the test so it states the line
itself. `templates/ADR.md` restates that test in its old words — "if the
decision affects multiple tickets or constrains future work, ADR it" — so the
wider reading the document no longer holds is still available one file away,
and the template is the file a contributor reaches for when writing a record.

Deferring this leaves the repository stating one test two ways that disagree,
which is the defect EM-016 and EM-016-001 were raised for on the README and
the document map, and which "Which document settles what" exists to prevent.

The evidence is the two texts side by side, read at the commit that closed
EM-019-001-001-001.

Deferral is acceptable while `docs/adr-process.md` is the document the policy
map names as settling this, which it is: a contributor following the map
reaches the corrected test. That is why this is `degraded` and not blocking.

## Context

Raised by the one independent review pass on EM-019-001-001-001 (finding
R1.4), which recorded it and routed it rather than repairing it, because that
ticket's Out of scope reserves `templates/ADR.md` to EM-018. EM-018 has
closed, so this child is raised to own it, under the second condition of
"When review ends".

## Specification

Documentation change only.

### Files

- `templates/ADR.md`, the closing sentence of "When to write an ADR vs not".

### Public surface

The template is copied by adopters. Its statement of the test is an
instruction they follow.

### Behaviour

- The template's statement of the test agrees with `docs/adr-process.md`, or
  names that document as settling it rather than restating it.
- Whichever is chosen, the template does not carry a second full statement
  of a rule the document states in full, per "Retiring a control": "A rule
  stated in two documents carries one falsifier, stated where the rule is
  stated in full and referenced from the other."

## Acceptance criteria

1. AC1: `templates/ADR.md` no longer states the superseded test.
2. AC2: the template and `docs/adr-process.md` give the same answer for
   EM-011's review-isolation rule and for ADR-0003, worked through whichever
   form the template ends up carrying.
3. AC3: no rule changes in `docs/adr-process.md`; this ticket amends the
   template only.
4. AC4: a change to a process document is `standard` on one independent
   review pass, per "The operative test"; the pass is recorded as one row of
   the Review table.

## Out of scope

- `docs/adr-process.md`. EM-019-001-001-001 settled the test there.
- Any other section of `templates/ADR.md`.

## References

- `templates/ADR.md`, "When to write an ADR vs not".
- `docs/adr-process.md`, "When to write one" — the corrected test.
- EM-019-001-001-001, Review, R1.4 — the finding this ticket is routed from.
- `docs/tier-review-model.md`, "Retiring a control" — the one-statement rule.

## Notes

The id was read with the next-id command as EM-023 corrected it: `git log
--full-history --diff-filter=AR --name-only --format= -- docs/tickets`, with
the EM-018 children extracted, returns `EM-018-001` alone, so `-002` is the
next free sequence.

## PR Description

### Ticket
EM-018-002 — The ADR template restates the decision-record test in its
superseded form.

### Tier
`standard`, on one independent review pass. `templates/ADR.md` states a
procedure a contributor performs and sits under `templates/`, which "The
operative test" names as a process document; the tier is fixed there and is
not the executor's to move. The pass ran against 7b34662 and is row 1 of the
Review table.

### Summary
The template closed with "if the decision affects multiple tickets or
constrains future work, ADR it" — the test in the form EM-019-001-001-001
removed from `docs/adr-process.md`, because on a literal reading it reaches
every rule added under an existing decision. The template now names the
document that states the test in full rather than carrying a second copy.

### Acceptance criteria
- [x] AC1: `templates/ADR.md` no longer states the superseded test. `grep -rn
  "multiple tickets\|constrains future work\|ADR it" templates/`, run after
  the repair commit, returns nothing.
- [x] AC2: the template and `docs/adr-process.md` give the same answer for
  EM-011's review-isolation rule and for ADR-0003, worked through the form the
  template now carries:
  - **EM-011's review-isolation rule** (`docs/quality-gates.md`, "Review
    isolation"). Document: named explicitly on the no-record side — "it says
    where the review ADR-0002 decided on runs, and was added under that
    decision". Template: no write-one bullet fires, because
    `docs/quality-gates.md` is not among the three the workflow bullet names,
    and no do-not bullet fires either; the reader is in doubt and follows the
    pointer, which returns no record. **Same answer.** It is reached by
    omission rather than by the test, which is part of what EM-018-003 owns.
  - **ADR-0003.** Document: on the record side — the falsifier obligation
    changed how every rule in `docs/` is written. Template: ADR-0003 landed
    "Retiring a control" in `docs/tier-review-model.md`, which the workflow
    bullet names, so a record is owed. **Same answer.**
- [x] AC3: no rule changes in `docs/adr-process.md`. `git diff main...HEAD
  --name-only`, run after the repair commit, names `templates/ADR.md`, this
  ticket file, the new EM-018-003 ticket and the board, and nothing under
  `docs/adr/` or `docs/adr-process.md`.
- [x] AC4: one independent review pass, run against 7b34662 by an agent that
  did not perform the work and did not receive the executor's reasoning,
  recorded as row 1 of the Review table below. It returned four must-fixes
  over six findings — three routed, and two notes repaired in the round.

### Falsification
N/A for a behavioural claim — this repository publishes documents and runs no
suite. Per criterion, what a reader does differently: a contributor in doubt
about whether their change needs a decision record is sent to the one place
the test is stated, instead of applying a copy in the template that the
document had already corrected.

For the findings repaired, per the contributor policy's §6 — both are notes,
which carry nothing under §6 as EM-009-001 narrowed it, and are recorded here
because their remedy changed the one line this ticket owns:
- R1.4 — the replacement sentence paraphrased the one-statement rule without
  naming `docs/tier-review-model.md`, "Retiring a control", and dropped its
  second clause. It was itself a second, unreferenced statement of a rule
  stated in full elsewhere, in the line this ticket exists to fix.
- R1.5 — the sentence asserted what the target contains, "with its falsifier
  and the line that says which rules it reaches", which can drift if that
  section is restructured, and the singular was wrong: the section carries two
  **Retired when:** lines. Both are gone. The sentence now names the section
  and the rule it acts under, and asserts nothing about the target's contents
  — which is the property a pointer is chosen for.

### Routed, not repaired
Three must-fixes are recorded and routed rather than repaired. All three land
on the two bullet lists above the sentence this ticket owns, and the ticket's
Files names only "the closing sentence of 'When to write an ADR vs not'", so
they lie inside a limit it records. Under the second condition of "When review
ends" they go to a ticket that owns them, raised because none existed:
**EM-018-003**. Those three must-fixes are discharged by raising it.

- **R1.1** (second column): the write-one list's fifth bullet fires on any
  workflow-rule change in three named documents, while the document says the
  trigger does not reach a rule added under an existing decision and works
  seven such rules as owing none. The wider reading this ticket removed from
  the closing sentence survives one list item above it, and a reader whose
  change matches the bullet is not in doubt and never reaches the pointer.
- **R1.2**: the same list omits the retirement clause entirely, so a rule
  retired or amended under "Retiring a control" matches no template trigger —
  and that is the one case where the document says the record *is* the
  control. It is also narrower on four items.
- **R1.3**: the lists are a second full statement of a rule the document
  states in full, carrying no falsifier and referencing nothing, which is what
  "Retiring a control" forbids. This ticket's Behaviour asks that the template
  not carry one; that is met for the test and not for the trigger list.

### Out of scope (per ticket)
Confirmed; nothing here exceeds it.
- `docs/adr-process.md` — untouched, which AC3 shows.
- Any other section of `templates/ADR.md` — untouched. The reviewer confirmed
  the edit is confined to the closing sentence.

### How to verify
1. `grep -rn "multiple tickets\|constrains future work" templates/` — nothing,
   which is AC1.
2. `sed -n '/When in doubt/,/Retiring a control/p' templates/ADR.md` — the
   pointer as it now stands.
3. `grep -n '^## When to write one' docs/adr-process.md` — the section the
   pointer names exists under exactly that heading.
4. `git diff main...HEAD --name-only` — nothing under `docs/adr/` or
   `docs/adr-process.md`, which is AC3.

### Risks / follow-ups
- **The pointer's adopter case, recorded not repaired.** An adopter who copies
  `templates/` without `docs/` now has a template whose only in-place
  tie-breaker is a pointer into a file they may not hold, where before it
  carried a self-contained rule of thumb. The reviewer checked this against
  EM-018, which settled the citing form, and found the pointer satisfies it:
  the template already cites `docs/ai-contributor-policy.md`,
  `docs/ticket-lifecycle.md` and `docs/tier-review-model.md` on the same
  terms, and `docs/adr-process.md` is published here. It is a residual EM-018
  already recorded in its own Risks, not a defect of this change.
- EM-018-003 will have to decide the adopter's case properly if it replaces
  the bullet lists with the pointer as well, since that would leave the
  template with no in-place statement at all. Its Behaviour says so.

### Review
One independent review pass, per "The operative test" for a change to a
process document. No second pass is taken.

| Round | Must-fix | Where (rules / lists / documents / tests) | Inside previous round's fix | Repaired by |
|---|---|---|---|---|
| 1 | 3 (of 6 findings) | documents: the template's fifth write-one bullet fires on any workflow-rule change while the document exempts a rule added under an existing decision, so the wider reading survives above the corrected sentence (must-fix, second column, routed to EM-018-003); the same list omits the retirement clause, where the document says the record is the control (must-fix, routed); the two bullet lists are a second full statement of a rule the document states in full, with no falsifier and no reference (must-fix, routed); the replacement sentence paraphrased the one-statement rule without naming it; the same sentence asserted what the target contains and said "its falsifier" where the section carries two; the adopter who copies only `templates/` is a residual EM-018 recorded | — | this commit |

Derived from the row and not asserted beside it: three must-fixes over one
review round, all three discharged by raising EM-018-003. Round 1 has no round
before it, so its inside-previous-fix cell reads `—` and no line is
uncountable.

- R1.1 · refuses · must-fix · `docs/adr-process.md`, "It does not reach a rule added inside a document, or extended in place one rule at a time, under an existing decision", and the seven rules it works as owing none · the template's fifth write-one bullet demands a record for any workflow-rule change in three named documents, including every rule added under an existing decision, so the reading this ticket removes survives one item above it and the pointer is never reached — remedy: the ticket owning the bullet lists replaces them with the pointer or aligns the bullet with the document; routed to EM-018-003; cost, if the remedy tightens a control: none — the remedy removes a demand for a record; inside previous fix: —
- R1.2 · permits · must-fix · `docs/adr-process.md`, the trigger "including a rule retired or amended under `docs/tier-review-model.md`, 'Retiring a control'" · no template bullet matches a retirement or amendment, which is the one case where the retired text leaves the document and the record is the only place it survives; the list is also narrower on four other items — remedy: routed to EM-018-003; cost, if the remedy tightens a control: an adopter considers a record on any workflow-rule change, which the document already asks; inside previous fix: —
- R1.3 · permits · must-fix · `docs/tier-review-model.md`, "Retiring a control", "A rule stated in two documents carries one falsifier, stated where the rule is stated in full and referenced from the other" · the two bullet lists are a second full statement of the document's trigger list, with no falsifier and no reference; this ticket's Behaviour is met for the test half and not the trigger half — remedy: routed to EM-018-003; cost: none; inside previous fix: —
- R1.4 · permits · note · `templates/ADR.md`, the replacement sentence · it paraphrased the one-statement rule without naming the document that states it, and dropped "and referenced from the other" — a second unreferenced statement in the line this ticket owns — remedy: name the section, or cut the justification; repaired; cost: none; inside previous fix: —
- R1.5 · permits · note · `templates/ADR.md`, the replacement sentence · it asserted what the target contains, which can drift, and said "its falsifier" where the section carries two **Retired when:** lines — remedy: shorten to the section name; repaired; cost: none; inside previous fix: —
- R1.6 · refuses · note · EM-018's Behaviour on citing files, and its Risks entry on an adopter copying only `templates/ADR.md` · the template's only in-place tie-breaker is now a pointer into a file an adopter may not hold — remedy: none required; the pointer satisfies EM-018's citing rule and the gap is that ticket's recorded residual; cost: none; inside previous fix: —

Both columns carry findings. The second-column ones are the more important:
R1.1 is a template demanding records the document refuses, which is
over-tightening, and it is ranked a must-fix of the same rank as a
first-column finding, as "What a review reports" requires.

### Definition of Done (all tiers)
The four machine checks do not apply to a repository that publishes documents
and runs no suite; the falsification gate is discharged above, with N/A for
the behavioural claim and the two repaired findings recorded. Every measured
figure names its baseline in the same sentence and is read from the command
named beside it. The independent pass a process-document change takes has run
and is recorded.
