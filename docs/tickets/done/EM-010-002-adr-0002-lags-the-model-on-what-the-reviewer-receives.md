---
id: EM-010-002
title: ADR-0002 lags the model on what the reviewer receives
status: done
tier: trivial
complexity: S
dependencies: [EM-010]
claimed_by: claude-fable-5-1
claimed_at: 2026-09-06
closed_at: 2026-09-06
---

# EM-010-002 — ADR-0002 lags the model on what the reviewer receives

## Context

Raised by the independent review of EM-010 (finding 7 of round 1). EM-010
amends `docs/tier-review-model.md` so that the reviewer receives the ticket,
the diff, the evidence and the two questions. ADR-0002 still says "given the
ticket and the diff but not the executor's reasoning" in its Decision and "a
reviewer reading only the ticket and the diff" in its Rationale. The model
is now a superset of the record; the record is not contradicted, but it is
the repository's decision history and lags the rule it decided.

**On the id.** This ticket is the second child of EM-010, not the first.
`EM-010-001` was created at 3da6c57 and renamed `EM-014-001` at 0947dda; the
tree shows no child of EM-010, and the next id is read from history per
`docs/ticket-lifecycle.md`, "Lineage". This is the first ticket numbered
under that rule.

## Specification

Documentation change only.

### Files

- `docs/adr/0002-critical-tier-review-in-a-single-maintainer-repository.md`

### Public surface

N/A — this repository publishes documents. No rule changes; a record is
brought up to date with the rule it recorded.

### Behaviour

- ADR-0002 is annotated in place, under a dated heading at the end, as EM-006
  annotated ADR-0038: the annotation states that EM-010 widened what the
  reviewer receives, quotes the two sentences as they stood, and points at the
  model's section. It also notes that EM-011 constrained where the reviewer
  works — a worktree of its own — which the ADR's "given the ticket and the
  diff" does not mention; routed here from EM-011's round-1 review, finding
  R1.9. The original text above the annotation is unchanged and the status
  stays `accepted`.

## Acceptance criteria

1. AC1: ADR-0002 carries a dated annotation naming EM-010 and the widened
   brief; the diff to the file is append-only.
2. AC2: The ADR's status is unchanged.

## Out of scope

- Superseding ADR-0002. The decision stands; one of its descriptive
  sentences is behind the model.

## References

- EM-010 — the widening.
- `docs/tier-review-model.md`, "Why 'another agent, human or AI'" and "What
  a review reports".
- EM-006 — the in-place annotation pattern, and the next-id-from-history
  rule this ticket's id follows.

## Notes

Trivial under the operative test: no rule or procedure changes; a record is
annotated.

## PR Description

### Ticket
EM-010-002 — ADR-0002 lags the model on what the reviewer receives

### Tier
`trivial` — a record annotated in place; no rule or procedure changes.
Self-merged, per the tier table.

### Summary
ADR-0002 carries a dated annotation at its end naming EM-010's widening of
the reviewer's brief and EM-011's worktree rule, quoting the two sentences
as they stood, and pointing at the model. Status unchanged.

### Acceptance criteria
- [x] AC1: a dated annotation naming EM-010 and the widened brief, with an
  append-only diff — `git diff HEAD~2..HEAD -- docs/adr/0002-*.md` shows
  additions only, below a horizontal rule.
- [x] AC2: the ADR's status is unchanged — `accepted`.

### Falsification
N/A — no behavioural claim. A reader of ADR-0002 learns the brief it
describes has grown and where the current description is.

### Out of scope (per ticket)
Confirmed: not superseded.

### How to verify
`tail -25 docs/adr/0002-*.md`; `head -5` shows the status line unchanged.

### Risks / follow-ups
This is the second annotated record after ADR-0038; the pattern is now
used twice and has no decision record of its own. If it recurs, that is a
process rule and takes a ticket.

### Review
N/A — trivial tier.

