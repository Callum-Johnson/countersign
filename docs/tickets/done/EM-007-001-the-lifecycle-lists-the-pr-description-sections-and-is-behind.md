---
id: EM-007-001
title: The lifecycle's list of pull-request description sections is behind the template
status: done
tier: trivial
complexity: S
dependencies: [EM-007]
claimed_by: claude-fable-5-1
claimed_at: 2026-09-06
closed_at: 2026-09-06
---

# EM-007-001 — The lifecycle's list of pull-request description sections is behind the template

## Context

Raised by the independent review of EM-007 (finding 2 of round 1).
`docs/ticket-lifecycle.md`, "Closing", step 1 enumerates what the appended
pull-request description contains: ticket, tier, summary, criteria with
evidence, out-of-scope confirmation, verification steps, risks and
follow-ups. `templates/PR-DESCRIPTION.md` has since gained a Falsification
section (EM-006) and a Review section (EM-007), and will gain more as the
wave lands. The two lists are the same fact stored twice, and only one of
them is maintained.

## Specification

Documentation change only.

### Files

- `docs/ticket-lifecycle.md` — "Closing", step 1.

### Public surface

N/A — this repository publishes documents. No rule changes.

### Behaviour

- Step 1 no longer enumerates the sections. It says the description follows
  `templates/PR-DESCRIPTION.md` and names the template as the one list, so
  the lifecycle cannot fall behind it again.

## Acceptance criteria

1. AC1: `docs/ticket-lifecycle.md`, "Closing", references the template
   instead of listing its sections.
2. AC2: No section name appears in the lifecycle that does not appear in the
   template.

## Out of scope

- Any change to the template. This ticket removes a duplicate, not a section.

## References

- `docs/ticket-lifecycle.md`, "Closing"
- `templates/PR-DESCRIPTION.md`
- EM-006, EM-007 — the sections whose addition exposed the drift

## Notes

Trivial under the operative test: the procedure is unchanged; one list is
replaced by a reference to the list it duplicated. ADR-0002's sentence that
changes to process documents are process-surface changes is read as applying
to changes that alter a rule or a procedure; this one alters neither, and
the executor re-tests the tier at claim and may raise it.

## PR Description

### Ticket
EM-007-001 — The lifecycle's list of pull-request description sections is
behind the template

### Tier
`trivial` — one list replaced by a reference to the list it duplicated;
no rule or procedure changes. Self-merged, per the tier table.

### Summary
"Closing", step 1, no longer enumerates the description's sections; it
names the template as the one list.

### Acceptance criteria
- [x] AC1: the lifecycle references the template — `docs/ticket-lifecycle.md`,
  "Closing", step 1, "in the form `templates/PR-DESCRIPTION.md` gives".
- [x] AC2: no section name in the lifecycle absent from the template —
  `grep -n "Falsification\|Review\|Risks" docs/ticket-lifecycle.md` finds
  no enumeration; the step names none.

### Falsification
N/A — no behavioural claim. A reader of the lifecycle's Closing step goes
to the template for the sections, and the lifecycle cannot fall behind it
again.

### Out of scope (per ticket)
Confirmed: the template is untouched.

### How to verify
`git diff HEAD~2..HEAD -- docs/ticket-lifecycle.md` — one step reworded.

### Risks / follow-ups
None.

### Review
N/A — trivial tier.

