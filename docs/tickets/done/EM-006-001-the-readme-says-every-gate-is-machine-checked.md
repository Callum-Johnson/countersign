---
id: EM-006-001
title: The README and the tier model say every gate is machine-checked; one now is not
status: done
tier: critical
complexity: S
dependencies: [EM-006]
claimed_by: claude-fable-5-1
claimed_at: 2026-09-06
closed_at: 2026-09-06
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

### Public surface

N/A — this repository publishes documents. The change corrects two sentences
and adds no rule.

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

### Ticket
EM-006-001 — The README and the tier model say every gate is
machine-checked

### Tier
`critical` — the tier model is a process surface (clause 5). Two sentences
corrected; no tier's review requirement changes.

**Independent review obtained**, per ADR-0002: a separate agent, given the
ticket, the diff and the two questions, and not the executor's reasoning,
reviewed the change in two rounds, read-only. Findings are under
Review; the tree was checked clean after each round.

### Summary
README idea 5 now says four gates are machine-checked and the fifth is a
count the executor reports and a reviewer verifies. The tier model's
sentence under the table says the four machine checks apply at every tier,
the falsification gate is discharged at every tier and independently
verified only where the tier summons a reviewer, and at `trivial` and
`standard` its count stands on the executor's word — a gap named, not
closed.

### Acceptance criteria
- [x] AC1: the README no longer says every gate is machine-checked —
  `README.md`, idea 5, "Four gates are machine-checked, and the fifth is
  countersigned."
- [x] AC2: the tier model says which gates are machine-checked and what
  happens to the falsification gate at tiers with no reviewer —
  `docs/tier-review-model.md`, "The tiers", the sentence after the table.
- [x] AC3: no tier's review requirement changes — the table is untouched;
  `git diff 630abdc..HEAD -- docs/tier-review-model.md` shows one
  paragraph edited.
- [x] AC4: independent review — see Review.

### Falsification
N/A — no behavioural claim. What a reader does differently, per criterion:
- AC1: a README reader does not quote the repository as claiming every
  gate is machine-checked.
- AC2: a standard-tier executor knows its recorded count is not
  independently verified, and a maintainer knows where that gap is.
- AC3: nothing; that is the guard working.

### Out of scope (per ticket)
Confirmed: the falsification gate is untouched; no tier newly summons a
reviewer; no seventh core idea — idea 5's heading is reworded and its
paragraph gains one sentence.

### Review
| Round | Must-fix | Where (rules / lists / documents / tests) | Inside previous round's fix | Repaired by |
|---|---|---|---|---|
| 1 | 1 (of 3 findings) | documents: the README's bold sentence claimed an unconditional countersignature the model provides at one tier of three (must-fix); the tier model restated the every-tier duty without a pointer; a reading that the gate is the reviewer's | — | 6e625db |
| 2 | 0 (of 1 note) | documents: one line left long by the pointer | 1 of 1 | the closing commit |

Derived total: 1 must-fix over two rounds.
Round 1 by column and rule — permits: R1.1, README idea 5 (remedy:
"countersigned where the work is"; the count reported at every tier and
verified where the tier summons a reviewer — a loosening of a claim, no
cost); R1.2, the tier model's sentence restating the every-tier duty
(remedy: a pointer to the quality gates). Refuses: R1.3, the same README
sentence read as making the gate the reviewer's (folded into R1.1's
rewrite: "which is why the count is written down"). Round 2's one note,
inside R1.2's remedy, is taken at close.
Post-review tree check after each round: `git status --porcelain` empty,
`git worktree list` showing only the main tree.

### How to verify
1. `grep -n "machine-checked" README.md docs/tier-review-model.md` — the
   README heading and the tier model's sentence, both qualified.
2. `git diff 630abdc..HEAD --stat` — two documents and ticket housekeeping.

### Risks / follow-ups
- The gap named here — a self-reported gate with no verifier at two tiers
  — is the maintainer's to close or accept. Closing it means the tier table
  summons a verifier for the count at `standard`, which is a change to what
  the tiers require and its own ticket.

