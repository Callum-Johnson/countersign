---
id: EM-020-001
title: A review must-fix on a sentence the ticket's Behaviour dictates is taken in the round and recorded
status: blocked
tier: critical
complexity: S
dependencies: [EM-021]
claimed_by: claude-fable-5-1
claimed_at: 2026-09-06
blocked_at: 2026-09-06
---

# EM-020-001 — A review must-fix on a Behaviour sentence is taken in the round and recorded

## Context

Raised by the independent review of EM-020 (round 2). Three closed tickets
carry a section headed "Departure from Behaviour, recorded": EM-007, whose
Behaviour dictated a sentence its own Context contradicted; EM-014-001,
whose Files and Behaviour disagreed about the record; and EM-020, whose
Behaviour dictated a falsifier that could never fire. In each, the review
named the defect and its remedy, the executor took the remedy in the
round, and the description recorded the departure under that heading. The
maintainer accepted the first two.

The contributor policy's §3 says otherwise: "The same applies when the
specification is wrong rather than unclear: raise a `BLOCKER:` explaining
what is wrong and what you would change. Do not unilaterally rewrite the
spec you were given." The practice has been to take the remedy the review
named and let the maintainer read it at close, which delivers the block's
answer without its latency. That is defensible, and it is not §3's letter,
and three instances clear the bar EM-021 sets for writing it down.

Either §3 gains the clause or the practice stops. Nothing written says
which.

## Specification

Documentation change only.

### Files

- `docs/ai-contributor-policy.md` §3.

### Public surface

N/A — this repository publishes documents. The change adds a clause to an
existing rule or confirms the rule as written.

### Behaviour

- §3 states when a wrong specification is repaired in the round rather than
  blocked: when an independent review has named the defect and its remedy,
  the remedy changes no decision the ticket makes, and the description
  records the departure under a heading of its own, quoting the sentence
  not followed. Outside those conditions §3 stands as written.
- The clause names the three instances.
- The clause states its falsifier: retired when a departure recorded under
  it is reversed by the maintainer at close more than once over a stated
  population; the practice is then delivering the wrong answer without the
  block's latency, and the block was cheaper.

## Acceptance criteria

1. AC1: §3 states the conditions under which a review-named remedy to a
   wrong specification is taken in the round, or states that it is not.
2. AC2: The clause names its instances and carries a **Retired when:**
   line.
3. AC3: Critical tier per ADR-0002: an independent agent that did not
   perform the work reviews this against the artifacts and records findings
   in two columns.

## Out of scope

- Reopening any of the three departures. Each was accepted or is before
  the maintainer in its own record.
- Any change to the blocking procedure itself.

## References

- `docs/ai-contributor-policy.md` §3 — the rule the practice departs from.
- EM-007, EM-014-001, EM-020 — the three instances, each under "Departure
  from Behaviour, recorded" in its description.
- EM-021 — the second-instance bar this ticket clears.

## Notes

Depends on EM-021 because it is the first rule raised under that bar, and
should be the first to cite it.

**BLOCKER (2026-09-06):** the executor cannot proceed. The ticket carries
two questions §3 reserves to the maintainer, found in one reading and stated
together as §3 asks.

1. **Whether §3 gains the clause.** The ticket does not say the decision is
   made: Context ends "Nothing written says which", AC1 admits "or states
   that it is not", and the EM-020 description that raised this ticket says
   "not decided here". Behaviour bullet 1 and AC2 presuppose the clause.
   Context and Behaviour therefore disagree on whether the choice exists,
   which is the disagreement §7 item 2 sends to §3. And the choice is not
   the executor's to make. The clause narrows §3, a control on the executor,
   over a class of cases; "Separation of duties" says the party subject to a
   control does not get to remove it, and "Retiring a control" says an
   amendment that loosens a rule is a retirement ticket not worked by the
   executor whose work the rule refused. The three departures the clause
   would license were each `claude-fable-5-1`'s, the executor this ticket is
   claimed by. Blocked on the precedent of EM-009-001, whose Specification
   narrowed a control on the executor by the same shape. The answers
   available: (a) §3 gains the clause as Behaviour states it, with its
   conditions, its three instances and its falsifier; (b) §3 stands as
   written and the practice stops, which is AC1's second arm, closes with no
   document change, and leaves the three departures as accepted exceptions
   that the description records; (c) a narrower clause in the maintainer's
   own wording, which replaces Behaviour bullet 1.
2. **If (a), the form and the hands.** "Retiring a control" makes a
   loosening an amendment with record: a decision record carrying §3's text
   as it stands, the finding that matched, and the new text. The Files list
   names no record, and EM-019-001-001, in `ready/`, owns whether a
   rule-adding ticket produces one. And the same section's last bullet
   would have this ticket worked by an executor other than the one the rule
   refused, which on this repository to date is every executor; the
   maintainer may waive that and say so, or work the amendment directly.

To proceed the executor needs the maintainer's answer to 1, and where it is
(a), to 2. Whichever answer comes is one count for or against §3's own
falsifier, which reads on blocks unblocked with the reading the executor
would have taken; that count is the maintainer's to keep.

## PR Description

> Leave this section empty when authoring the ticket.
