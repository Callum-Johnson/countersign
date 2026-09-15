---
id: EM-007-002-003-002-001
title: The annotation preambles have no canonical form and two carry the stale wording
status: ready
tier: standard
kind: defect
impact: degraded
delivery: maintenance
why: "Without a canonical form, the next annotation on any record has four wordings to choose between and one record has none at all, and two records still carry the relative status claim that goes stale the moment a status moves."
complexity: S
dependencies: [EM-007-002-003-002]
claimed_by:
claimed_at:
blocked_at:
closed_at:
---

# EM-007-002-003-002-001 — The annotation preambles have no canonical form

## Why this ticket should be worked

The affected outcome is whether a contributor annotating a decision record has
one form to copy.

`docs/adr/` carries six annotations across four records. Their preambles take
four distinct forms and one record's annotation has no preamble at all, varying
on three axes: the opener ("Not part of the decision as recorded" against "This
section is not part of the decision as recorded"), the assurance ("The text
above the horizontal line is unchanged" against "Everything above the
horizontal line is the original text"), and the status clause ("the status
stays `accepted`" against "the status is unchanged" against ADR-0004's
two-sentence historical form).

Two of them carry the relative wording — "the status is unchanged" — which
EM-007-002-003-002 found has two readings and goes stale the moment the status
it describes moves. Neither is false today, because neither record's status has
moved since. That is why this is `degraded` rather than blocking: the defect is
latent in ADR-0002's first annotation and ADR-0003's, and it fires only when
one of those records transitions.

The evidence is the six preambles read together, quoted in EM-007-002-003-002's
description under AC3, which is where the comparison was made.

Deferral is acceptable while no record carrying that wording changes status. It
stops being acceptable the first time one does.

## Context

Raised from the one independent review pass on EM-007-002-003-002, which
carried out AC3's comparison and found that a further ticket is owed. That
ticket's Out of scope reserves every other record's annotation "except to read
it for AC3", so the repair goes to a ticket of its own.

EM-007-002-003-002 also introduced a fourth form, specific to ADR-0004, which
no other annotation can copy — so settling the canonical form is part of the
work rather than only correcting the two stale wordings.

## Specification

Documentation change only.

### Files

- `docs/adr/0002-critical-tier-review-in-a-single-maintainer-repository.md` —
  the 2026-09-06 EM-010-002 annotation's preamble, and the 2026-09-06 EM-017
  annotation, which has none.
- `docs/adr/0003-every-rule-states-its-falsifier-and-a-control-can-be-retired.md`
  — the 2026-09-10 annotation's preamble.
- `docs/adr-process.md` — only if the canonical form is written down as a rule
  rather than left as a form the records exhibit. Whether it should be is the
  ticket's to decide, and if it is, the second-instance bar and the
  falsifier obligation both apply.

### Public surface

N/A — this repository publishes documents.

### Behaviour

- No annotation preamble states a status claim that goes stale when the status
  moves. The historical form — what the status read when the annotation was
  written, and what moved it since, if anything — does not.
- The annotation that has no preamble gains one, or the ticket records why an
  annotation may omit it.
- The description states the canonical form and where a contributor finds it,
  so that the next annotation has one thing to copy.
- A dated annotation is not rewritten to say something it did not say. Where a
  preamble's description of the file has gone stale, the amendment says on
  whose ticket it was made, as ADR-0004's now does; where a finding has gone
  stale, a new annotation carries the correction. EM-023-001 draws that line.

## Acceptance criteria

1. AC1: no preamble under `docs/adr/` claims the status is unchanged in the
   relative form.
2. AC2: every annotation under `docs/adr/` carries a preamble, or the
   description says why one does not.
3. AC3: the canonical form is stated in the description, and each preamble is
   shown to match it or its divergence is explained.
4. AC4: each amended preamble names the ticket that amended it, per
   EM-023-001's line.
5. AC5: a change to a process document is `standard` on one independent review
   pass, per "The operative test"; the pass is recorded as one row of the
   Review table.

## Out of scope

- ADR-0004's annotations, which EM-007-002-003-002 settled.
- Any decision any record holds, and any status value.
- `examples/adr/adr-0038`'s annotations, which EM-023-001 and EM-023-002
  settled and which `DISCLOSURE.md` counts.

## References

- EM-007-002-003-002, description, AC3 — the six-preamble comparison.
- EM-023-001 — a dated annotation is appended to, not rewritten.
- `docs/adr-process.md`, "Structure" — the status transition.
- `docs/tier-review-model.md`, "Retiring a control" — the falsifier obligation,
  if a rule is written.

## Notes

The id was read with the next-id command as EM-023 corrected it: `git log
--full-history --diff-filter=AR --name-only --format= -- docs/tickets`, with
the EM-007-002-003-002 children extracted, returns nothing, so `-001` is free.

## PR Description

> Leave this section empty when authoring the ticket.
