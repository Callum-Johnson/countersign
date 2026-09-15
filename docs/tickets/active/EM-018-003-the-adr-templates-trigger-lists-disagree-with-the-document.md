---
id: EM-018-003
title: The ADR template's trigger lists disagree with the document in both directions
status: in-progress
tier: standard
kind: defect
impact: degraded
delivery: maintenance
why: "Without aligning them, the template tells a contributor to write a record where the document says none is owed, and stays silent where the document says the record is the control."
complexity: S
dependencies: [EM-018-002]
claimed_by: claude-opus-5
claimed_at: 2026-09-15
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

> Leave this section empty when authoring the ticket.
