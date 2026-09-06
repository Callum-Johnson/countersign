---
id: EM-019-001-001
title: Rule-adding tickets produce no decision record, against the trigger list
status: ready
tier: standard
complexity: S
dependencies: []
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
- The rule states its falsifier.

## Acceptance criteria

1. AC1: `docs/adr-process.md` states what "a workflow rule changes"
   reaches, with an example on each side of the line.
2. AC2: The seven rule-adding tickets that produced no record are either
   consistent with the stated line, or named in the pull-request
   description as a gap the decision accepts.
3. AC3: The trigger carries a **Retired when:** line.
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

Proposed `standard`: it makes an existing trigger precise and adds no
obligation. EM-007-002 owns the question of whether that proposal should be
`critical` instead.

## PR Description

> Leave this section empty when authoring the ticket.
