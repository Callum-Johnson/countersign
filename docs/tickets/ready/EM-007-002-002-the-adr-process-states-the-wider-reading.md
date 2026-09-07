---
id: EM-007-002-002
title: The ADR process still says changing the process is critical, which now reads wider than the model
status: ready
tier: critical
complexity: S
dependencies: [EM-007-002]
---

# EM-007-002-002 — The ADR process states the wider reading the model no longer holds

## Context

Raised while working EM-007-002, under the contributor policy's §4, from
the independent review of 49b5c00 (finding R1.5 of round 1).

`docs/adr-process.md`, "Decisions about the process are themselves ADRs",
says:

> The ticket lineage scheme, the tier trigger, and the review model each
> have a decision record. Changing the process is a process-surface change,
> which the operative test classifies as `critical`, which means it needs a
> second reviewer.

EM-007-002 narrows what the operative test classes as `critical` on a
process document: the change must add, alter or retire a rule or a
procedure. The sentence above now reads wider than the model it cites, in
exactly the way ADR-0002's Context did before EM-007-002 annotated it.
A contributor who reads this section and stops there gets `critical` for a
typo fix in a process document; a contributor who reads the model gets
`trivial`. Two published statements again give different answers for the
same change, which is the defect EM-007-002 was raised to remove.

The section's own falsifier does not answer it either. It reads:

> **Retired when:** the tier model ceases to class the process surface as
> `critical`, at which point this rule's second sentence is false and its
> first stands alone.

The model has not ceased to class the process surface as `critical`; it has
narrowed which process-document changes are on that surface. So the
falsifier is not matched, the retirement path of
`docs/tier-review-model.md`, "Retiring a control", is not triggered, and
the mismatch has nowhere to go but a ticket.

EM-007-002 did not repair this. Annotating or amending a rule in a second
process document is a rule change of its own under the very line EM-007-002
writes, and would have widened that ticket past the two documents its
acceptance criteria name. The judgement is recorded in EM-007-002's
pull-request description.

## Specification

Documentation change only. One section of one document is made to agree
with the model it cites.

### Files

- `docs/adr-process.md` — "Decisions about the process are themselves
  ADRs": the second sentence, and its **Retired when:** line if the
  reworded sentence needs a different one.

### Public surface

N/A — this repository publishes documents.

### Behaviour

- The section's second sentence returns the same tier as
  `docs/tier-review-model.md`, "The operative test", for a change to a
  process document that moves no rule and no procedure.
- The section's first sentence and its argument — that a governance system
  changed silently is not a control — are unchanged. What is wrong is the
  tier claim, not the claim that process changes are recorded.
- The **Retired when:** line names evidence that could be recognised
  against the sentence as reworded; if the current line still fits, it is
  kept and the ticket says why.
- No new rule enters, so the second-instance bar of
  `docs/tier-review-model.md`, "A rule needs a second instance", is not
  engaged; if the repair adds one, that ticket names its instances.

## Acceptance criteria

1. AC1: the section, read on its own, gives the same answer as the
   operative test for a change to a process document that moves no rule and
   no procedure.
2. AC2: the section's first sentence, its three named records, and its
   closing argument are unchanged.
3. AC3: the section carries a **Retired when:** line that matches the
   sentence as it then stands.
4. AC4: `docs/tier-review-model.md` is unchanged by this ticket.
5. AC5: an independent agent reviews this and records findings in two
   columns.

## Out of scope

- `docs/tier-review-model.md`, and the line EM-007-002 writes into it.
- "When to write one" and the line beneath it, which is EM-019-001-001-001.
- Whether ADR-0002's Context is amended rather than annotated.

## References

- `docs/adr-process.md`, "Decisions about the process are themselves ADRs".
- `docs/tier-review-model.md`, "The operative test" — the paragraph
  beginning **A change to a process document**.
- ADR-0004 — the record of the decision that created the mismatch.
- EM-007-002, round 1, finding R1.5 — where this was found.
- EM-019-001-001-001 — the other unreconciled sentence in the same
  document, in a different section.

## Notes

Proposed `critical`: the change alters a rule in a process document, which
is `critical` by the paragraph EM-007-002 adds to the operative test. An
author may raise and may never lower.

## PR Description

> Leave this section empty when authoring the ticket.
