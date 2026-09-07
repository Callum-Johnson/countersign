---
id: EM-022-001
title: Update ticket examples for rationale and impact metadata
status: blocked
tier: trivial
kind: maintenance
impact: enhancement
delivery: maintenance
why: "Without updated examples, adopters can copy ticket forms that omit newly required rationale and impact metadata."
complexity: S
dependencies: []
claimed_by:
claimed_at:
blocked_at: 2026-09-07
closed_at:
---

# EM-022-001 — Update ticket examples for rationale and impact metadata

## Why this ticket should be worked

The published ticket template sends contributors to worked examples that
predate the proposed `kind`, `impact`, `delivery`, `why` and causal
justification requirements. Leaving those examples unchanged would give an
adopter two incompatible forms to copy.

Evidence: the examples under `examples/tickets/` contain the existing
frontmatter shape and no `## Why this ticket should be worked` section.
Deferral is acceptable until EM-022 merges because the template continues to
be the current authoritative form.

BLOCKER: EM-022 must merge before examples can truthfully demonstrate its
required ticket form. Unblock when that rule is present on the default branch.

## Context

EM-022 proposes the new portable ticket fields and cites
`examples/tickets/PRJ-001-repo-skeleton.md` as a fully worked example in the
ticket template. This is a documentation follow-up discovered while applying
that change.

## Specification

### Files

- `examples/tickets/*.md` — add accurate `kind`, `impact`, `delivery` and
  `why` fields, plus the causal justification section, without changing each
  example ticket's recorded implementation evidence.

### Behaviour

- Every ticket example follows the post-EM-022 template shape.
- Historical facts remain described as historical rather than being invented
  to satisfy a new field.

## Acceptance criteria

1. Every published ticket example has all metadata and the causal
   justification section required by EM-022.
2. The examples do not change their recorded completion, review or test
   evidence.

## Out of scope

- Changing the ticket template or lifecycle rule. EM-022.
- Reclassifying real tickets outside `examples/tickets/`.

## References

- EM-022
- `templates/TICKET.md`, "Example: filled ticket"

## Notes

N/A.

## PR Description

> Leave this section empty when authoring the ticket.
