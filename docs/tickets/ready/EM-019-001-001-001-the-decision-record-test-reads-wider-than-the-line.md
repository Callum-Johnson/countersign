---
id: EM-019-001-001-001
title: The decision-record test reads wider than the line drawn beneath it
status: ready
tier: critical
complexity: S
dependencies: [EM-019-001-001]
---

# EM-019-001-001-001 — The decision-record test reads wider than the line

## Context

Raised by the independent review of EM-019-001-001 (finding R1.4 of round
1).

`docs/adr-process.md`, "When to write one", states a test: "if the decision
affects multiple tickets or constrains future work, it is an ADR. If it
affects only the ticket in hand, the ticket is enough." EM-019-001-001 draws
a line beneath it under which a rule added inside a document under an
existing decision owes no record, and says how the test reads under the
line: the constraint such a rule places on future work is the existing
decision's. On a literal reading the test still reaches every such rule —
each constrains future work — so the section carries a test and a gloss on
the test, and a reader who stops at the test gets the wider answer.

EM-019-001-001's Out of scope reserves the test and every other trigger, so
the gloss is what that ticket could do. Rewording the test is this one.

## Specification

Documentation change only.

### Files

- `docs/adr-process.md` — "When to write one", the test sentence and the
  gloss on it in the paragraph beginning **What "a workflow rule changes"
  reaches**.

### Public surface

N/A — this repository publishes documents. One sentence is made to agree
with the line beneath it.

### Behaviour

- The test sentence, read on its own, gives the same answer the line gives:
  a decision that changes how the process is governed, or constrains work
  beyond the ticket in hand and sits under no decision already recorded, is
  a record; a rule added under a recorded decision is not, whatever it
  constrains.
- The gloss — "The test above reads the same way" and the clause that
  follows it — is removed, since a test that says what it means needs no
  gloss.
- This ticket amends a sentence and adds no rule, so it states no new
  falsifier: the test retires with the trigger list's existing **Retired
  when:**, and the line with its own. The second-instance bar in
  `docs/tier-review-model.md`, "Retiring a control", governs a rule's entry
  as a ticket's own subject and does not reach this amendment.

## Acceptance criteria

1. AC1: the test sentence, read without the paragraph beneath it, places
   EM-011's review-isolation rule on the no-record side and ADR-0003 on the
   record side.
2. AC2: the gloss on the test is gone from the line's paragraph, and the
   line's examples and falsifier are unchanged.
3. AC3: An independent agent reviews this and records findings in two
   columns.

## Out of scope

- The line itself, its examples and its falsifier.
- Any other trigger in the list, and the section's existing **Retired
  when:**.
- `templates/ADR.md`, which restates the trigger; EM-018 owns the
  templates.

## References

- `docs/adr-process.md`, "When to write one".
- EM-019-001-001 — the line, and the review finding this ticket records.
- ADR-0003 and EM-011 — the two examples the test must agree with.

## Notes

Proposed `critical`: `docs/adr-process.md` is a process document, which
ADR-0002 classifies as process-surface, and an author may raise but never
lower. EM-007-002 owns whether that classification is right.

## PR Description

> Leave this section empty when authoring the ticket.
