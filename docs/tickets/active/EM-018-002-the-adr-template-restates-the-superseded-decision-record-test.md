---
id: EM-018-002
title: The ADR template restates the decision-record test in its superseded form
status: in-progress
tier: standard
kind: defect
impact: degraded
delivery: maintenance
why: "Without correcting it, the repository states one test two ways that disagree, and the template carries the wider reading that EM-019-001-001-001 removed from the document it restates."
complexity: S
dependencies: [EM-019-001-001-001]
claimed_by: claude-opus-5
claimed_at: 2026-09-15
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

> Leave this section empty when authoring the ticket.
