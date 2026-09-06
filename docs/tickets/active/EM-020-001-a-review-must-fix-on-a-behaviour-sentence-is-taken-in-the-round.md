---
id: EM-020-001
title: A review must-fix on a sentence the ticket's Behaviour dictates is taken in the round and recorded
status: in-progress
tier: critical
complexity: S
dependencies: [EM-021]
claimed_by: claude-fable-5-1
claimed_at: 2026-09-06
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

## PR Description

> Leave this section empty when authoring the ticket.
