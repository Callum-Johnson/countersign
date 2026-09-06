---
id: EM-019-001-001
title: Rule-adding tickets produce no decision record, against the trigger list
status: in-progress
tier: critical
complexity: S
dependencies: []
claimed_by: claude-fable-5-1
claimed_at: 2026-09-06
---

# EM-019-001-001 — Rule-adding tickets produce no decision record

## Context

Raised by the independent review of EM-019-001 (finding R1.6 of round 1).

`docs/adr-process.md` lists "A workflow rule changes" as a trigger for a
decision record, and gives the test: "if the decision affects multiple
tickets or constrains future work, it is an ADR". Five tickets closed in
this repository add a rule to a process document and produce no record —
EM-008, EM-009, EM-010, EM-011, EM-012 — and EM-016 and EM-019-001 add one
each. The repository holds three decision records, all of them decisions
*about* the process rather than rules within it.

Either the trigger means something narrower than it says, or the practice
has been wrong seven times. Nothing written down says which, so a
contributor reading the trigger list cannot tell whether their rule-adding
ticket owes a record.

## Specification

Documentation change only.

### Files

- `docs/adr-process.md` — "When to write one".

### Public surface

N/A — this repository publishes documents. One trigger is made precise.

### Behaviour

- The trigger says what "a workflow rule changes" reaches: a decision that
  changes how the process itself is governed, as against a rule added
  inside a document under an existing decision. The practice this
  repository has followed is the second, and the document says so.
- Where the line falls is stated with an example on each side: ADR-0003
  (the falsifier obligation, which changed how every rule is written) on
  one, and EM-011's review-isolation rule (added under the existing review
  model) on the other.
- **The falsifier of the line this ticket draws:** retired when a rule
  added under an existing decision, and therefore recorded nowhere, is
  found to have been undone or contradicted by a later contributor who
  could not see why it was there, more than once over a stated population
  of merged changes. The line is then drawn too narrowly and the trigger
  should reach those rules after all.

## Acceptance criteria

1. AC1: `docs/adr-process.md` states what "a workflow rule changes"
   reaches, with an example on each side of the line.
2. AC2: The seven rule-adding tickets that produced no record are either
   consistent with the stated line, or named in the pull-request
   description as a gap the decision accepts.
3. AC3: The line this ticket draws carries its own **Retired when:**
   line, distinct from the one the trigger list already has at baseline.
4. AC4: An independent agent reviews this and records findings in two
   columns.

## Out of scope

- Writing decision records retrospectively for the seven. If the answer is
  that they owed one, that is a separate ticket, and ADR-0001's rejection
  of backdating applies to how it is done.
- Any other trigger in the list.

## References

- `docs/adr-process.md`, "When to write one".
- EM-008, EM-009, EM-010, EM-011, EM-012, EM-016, EM-019-001 — the
  rule-adding tickets that produced no record.
- ADR-0003 — the one rule-level decision that did.

## Notes

Proposed `critical`: `docs/adr-process.md` is a process document, which
ADR-0002 classifies as process-surface, and an author may raise but never
lower. EM-007-002 owns whether that classification is right; until it is
answered, the tier that does not remove a control is the one to propose.

## PR Description

> Leave this section empty when authoring the ticket.
