---
id: EM-024-001
title: The tier model restates a count beside its own list
status: ready
tier: standard
complexity: S
dependencies: [EM-024]
---

# EM-024-001 — The tier model restates a count beside its own list

## Context

EM-024 lands `docs/quality-gates.md`, "A count that describes the tree lives
in a test", which asks that a count describing the tree have one site and that
every other mention name the site rather than the number. The first thing that
section binds is this repository, and one sentence in it does not comply.

`docs/tier-review-model.md`, "Retiring a control", in the paragraph beginning
"**A rule needs a second instance**", reads: "Of the thirteen rule-adding
tickets from EM-006 to EM-020, eight name one source ticket on one project in
their Context — EM-007, EM-008, EM-010, EM-011, EM-012, EM-012-001, EM-014-001
and EM-019-001 — counted by reading each Context for the source it names."
Two counts, two defects, one sentence:

- **"eight" is restated beside its own list.** The enumeration that follows it
  is the site. The number is a second copy of what the list already says, and
  the two can disagree the moment a ticket is added to or removed from the
  list — which is exactly the shape EM-024's Context records four times over.
- **"thirteen" has no site at all.** No list, no command, no test. It is the
  kind of number EM-024 was raised about: a reader who doubts it must
  reconstruct the population "rule-adding tickets from EM-006 to EM-020" by
  hand, which is the work the sentence's own closing clause admits to.

Found on 2026-09-08 while working EM-024, by reading the document the new
section binds. The location is read from
`grep -n "thirteen rule-adding" docs/tier-review-model.md`, which returns line
490 at `3e8a34b`.

## Specification

The sentence keeps its evidence and loses its unpinned numbers. Two changes,
independently decidable by the executor:

- The enumeration stays and "eight" goes, or "eight" stays and the enumeration
  moves to a site the sentence points at. The first is the cheaper reading and
  is what OMN-024's round 3 chose for its own sibling list; the ticket does not
  mandate it.
- "thirteen" either gains, in the same sentence, the command that produces it
  with its baseline — the population is a range of ticket ids, so a command
  over `git log --diff-filter=A --name-only --format= -- docs/tickets` can be
  written — or the sentence drops the count and names the range it already
  names, letting the reader count if the reader cares.

Nothing else in the paragraph changes. The rule the paragraph states, the
second-instance bar, is not touched; this is its evidence sentence only.

### Files

- `docs/tier-review-model.md`, "Retiring a control" — the paragraph beginning
  "**A rule needs a second instance**"

### Public surface

None added. The sentence is the published evidence for a rule an adopter
follows, so what an adopter reads is the correctness of the evidence, not a
new instruction.

### Behaviour

- After the change no number in that sentence lacks a site a reader can open
  or a command a reader can run.
- **This ticket adds no rule, so it states no falsifier.** The rule it applies
  is EM-024's, which carries its own.
- The map and the model's index are not touched: no section is added, removed
  or renamed, and the question the row settles does not move.

## Acceptance criteria

1. AC1: the sentence no longer states "eight" beside the list that enumerates
   the same eight, or states it with the list named as its one site.
2. AC2: "thirteen" is either produced by a command the sentence names, with
   its baseline in the same sentence, or is gone.
3. AC3: the paragraph's rule — the second-instance bar — is unchanged, shown
   by the diff.

## Out of scope

- Every other number in this repository's documents. `README.md`'s two commit
  counts for one project are EM-015's and are not touched here.
- A sweep of the repository for counts without a site. EM-024's Out of scope
  left whether that is worth doing open, and this ticket does not decide it.
- `docs/quality-gates.md`, "A count that describes the tree lives in a test",
  itself. If that section is wrong, the finding belongs to EM-024.

## References

- `docs/quality-gates.md`, "A count that describes the tree lives in a test" —
  the rule this applies
- EM-024 — the ticket that landed it, and the instances in its Context
- EM-015 — the other count defect on this board, on figures no command in this
  repository can produce, which is why it is a different repair

## Notes

Raised under the contributor policy's §4 while working EM-024: found, not
fixed in place. The instance is worth having on the record for a second
reason — it is the first evidence that the new section catches something in
this repository, which is the population its falsifier will eventually be read
over.
