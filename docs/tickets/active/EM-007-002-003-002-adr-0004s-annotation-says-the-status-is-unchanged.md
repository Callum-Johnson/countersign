---
id: EM-007-002-003-002
title: ADR-0004's annotation says the status is unchanged and the status has changed
status: in-progress
tier: standard
kind: defect
impact: degraded
delivery: maintenance
why: "Without correcting it, ADR-0004 states in its own text that its status is unchanged while the line above carries a changed value, and nothing in the file lets a reader order the two."
complexity: S
dependencies: [EM-007-002-003-001]
claimed_by: claude-opus-5
claimed_at: 2026-09-15
blocked_at:
closed_at:
---

# EM-007-002-003-002 — ADR-0004's annotation says the status is unchanged

## Why this ticket should be worked

The affected outcome is whether ADR-0004 can be read without the reader having
to guess which of two sentences is current.

Its 2026-09-15 annotation opens: "Not part of the decision as recorded. The
text above the horizontal line is unchanged, and the status is unchanged."
EM-007-002-003-001 changed the status from `proposed` to `accepted` on the
same date, above that rule. The record now carries both.

The sentence has two readings and the file supports neither over the other.
Narrowly it describes what the annotation did — that annotation did not change
the status, which is true and stays true. Broadly it is a standing claim about
the record, which is now false. The sibling preambles on ADR-0001 and ADR-0002
say "the status stays `accepted`", which is unambiguously the broad reading
and remains true of those records; ADR-0004's wording is the one that does not
describe its own file.

Deferring this leaves a self-contradicting record whose subject is the tier of
every process-document change — the record contributors reach for most. It is
`degraded` rather than blocking because the status line itself is correct and
the decision is untouched; only the annotation's description of the file is
stale.

## Context

Raised by the one independent review pass on EM-007-002-003-001 (finding
R1.2), which recorded it and routed it rather than repairing it: the remedy
lies inside that ticket's own stated limits — Behaviour, "The body of the
record and its annotation are untouched", and Out of scope, "any part of its
body" — so under the second condition of "When review ends" it goes to a
ticket that owns it, raised because none existed.

## Specification

Documentation change only.

### Files

- `docs/adr/0004-a-process-document-change-is-standard-on-one-pass.md`, the
  2026-09-15 annotation's preamble, or a new annotation below it.

### Public surface

N/A — this repository publishes documents.

### Behaviour

- The record no longer asserts that its status is unchanged while carrying a
  changed one.
- Whichever form is chosen, the 2026-09-15 annotation's substance is not
  rewritten: either its preamble gains a clause naming the later transition
  and the ticket that made it, or a new dated annotation below its own rule
  records the transition. A dated annotation is not edited to say something
  it did not say, per EM-023-001.
- The wording chosen says which of the two readings the preamble carries, so
  the next annotation on any record has one form to copy.

## Acceptance criteria

1. AC1: no sentence in ADR-0004 claims the status is unchanged while the
   status line reads a value it did not carry when that sentence was written.
2. AC2: the 2026-09-15 annotation's substance is unchanged; any addition is a
   clause naming the transition, or a new annotation below a rule of its own.
3. AC3: the preambles of the annotations on ADR-0001, ADR-0002, ADR-0003 and
   ADR-0004 are compared, and the description says whether they now state the
   same thing the same way or whether a further ticket is owed.
4. AC4: a change to a process document is `standard` on one independent
   review pass, per "The operative test"; the pass is recorded as one row of
   the Review table.

## Out of scope

- The status value itself, which EM-007-002-003-001 settled, and the decision
  ADR-0004 records.
- Any other record's annotation, except to read it for AC3.

## References

- `docs/adr/0004-...md`, the 2026-09-15 annotation.
- EM-007-002-003-001, Review, R1.2 — the finding this is routed from.
- EM-023-001 — that a dated annotation is appended to, never edited.
- ADR-0001 and ADR-0002, whose preambles use "the status stays `accepted`".

## Notes

The id was read with the next-id command as EM-023 corrected it: `git log
--full-history --diff-filter=AR --name-only --format= -- docs/tickets`, with
the EM-007-002-003 children extracted, returns `EM-007-002-003-001` alone.

## PR Description

> Leave this section empty when authoring the ticket.
