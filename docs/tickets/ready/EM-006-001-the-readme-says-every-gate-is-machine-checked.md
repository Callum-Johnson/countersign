---
id: EM-006-001
title: The README and the tier model say every gate is machine-checked; one now is not
status: ready
tier: critical
complexity: S
dependencies: [EM-006]
---

# EM-006-001 — The README and the tier model say every gate is machine-checked

## Context

Raised by the independent review of EM-006 (finding 2 of round 1). EM-006
adds the falsification gate to `docs/quality-gates.md` as "a fifth gate that
no tool runs": an executor obligation, discharged by the executor and
verified at review. Two published sentences now contradict it:

- `README.md`, core idea 5: "Gates are machine-checked … An agent cannot talk
  its way past a failing gate."
- `docs/tier-review-model.md`, "The tiers": "There is no tier that skips the
  machine checks — the tier governs *human and peer* review, not automated
  review."

Both were true at 8b0a8b4 and are now incomplete: the falsification gate is
self-reported, which is a gate an agent *can* talk past, and the only thing
that stops it is the reviewer verifying the recorded count. EM-006 put the
README out of its own scope and did not touch the tier model; the
contradiction is recorded here rather than fixed there.

## Specification

Documentation changes only.

### Files

- `README.md` — core idea 5.
- `docs/tier-review-model.md` — the sentence under the tier table.

### Behaviour

- README idea 5 states that four gates are machine-checked and the fifth is
  reported by the executor and verified by the reviewer, in one or two
  sentences, without restating the gate.
- The tier model's sentence says the same in its own terms: the machine gates
  apply at every tier; the falsification gate is discharged at every tier and
  independently verified only where the tier summons a reviewer.
- Neither change alters what any tier requires. If the maintainer decides the
  falsification gate should be reviewer-verified at every tier, that is a
  change to the tier table and a separate ticket.

## Acceptance criteria

1. AC1: `README.md` idea 5 no longer states that every gate is machine-checked.
2. AC2: `docs/tier-review-model.md` states which gates are machine-checked and
   what happens to the falsification gate at tiers with no reviewer.
3. AC3: No tier's review requirement changes.
4. AC4: Critical tier per ADR-0002 — the tier model is a process surface: an
   independent agent reviews this against the artifacts and records findings
   in the pull-request description.

## Out of scope

- Any change to the falsification gate itself (EM-006), or to which tiers
  summon a reviewer.
- The seventh-core-idea question EM-006's Out of scope names. This ticket
  corrects a sentence; it does not add one.

## References

- EM-006 — the gate, and its Out of scope, which excluded the README.
- `docs/quality-gates.md`, "The falsification gate".
- `README.md`, "The core ideas".

## Notes

Trivial in size, critical in tier: the tier model is a process surface under
clause 5 of the operative test, and a README claim about how gates work is
the kind of sentence a reader adopting the model quotes.

## PR Description

> Leave this section empty when authoring the ticket.
