---
id: EM-004
title: Add per-project case studies
status: blocked
tier: standard
complexity: M
dependencies: [EM-002]
claimed_by: claude-fable-5-1
claimed_at: 2026-09-06
blocked_at: 2026-09-06
---

# EM-004 — Add per-project case studies

## Context

`case-studies/00-growth-2024-2026.md` compares three projects across a table
and a few paragraphs each. It establishes the trajectory but not the
engineering: a reader who wants to know what was actually built, and what was
hard about it, has nowhere to go.

The constraint from EM-001 applies unchanged. Two of the three projects
implement a third party's ruleset, and no case study may describe the domain.

## Specification

One case study per project, each describing the engineering problem and the
approach, and none describing the domain.

### Files

- `case-studies/01-deterministic-systems.md` — determinism, seeded
  reproducibility, pure-function resolution, explanation traces, and why
  replayability constrains the architecture.
- `case-studies/02-contract-first-client.md` — a thin client against an
  authoritative backend: versioned contracts, compatibility discipline,
  integration testing, and avoiding duplicated business logic.
- `case-studies/03-applied-ai-product.md` — multi-provider model design,
  structured outputs, validation and normalisation, cost and token telemetry,
  separation of user data, and human review boundaries.

### Behaviour

- Each names the engineering problem, the approach, and at least one thing
  that was got wrong first.
- No domain vocabulary, no rules content, no product internals, no
  credentials or customer data.
- Metrics are stated only where verifiable from the repository.

## Acceptance criteria

1. AC1: Three case studies exist and are linked from the README.
2. AC2: The proprietary-term scan returns zero matches against them.
3. AC3: Each contains at least one thing that went wrong and what changed.
4. AC4: Every metric is traceable to a repository artifact.

## Out of scope

- Screenshots or architecture diagrams of any private product.
- Naming either private project.

## References

- `DISCLOSURE.md`
- `case-studies/00-growth-2024-2026.md`

## Notes

AC3 is the point of the ticket. Case studies that describe only successes
read as marketing, and the growth case study already sets the expectation
that this repository records what it got wrong.

**BLOCKER (2026-09-06):** every sentence this ticket asks for is about a
private project the executor cannot read. The engineering problem, the
approach, the thing got wrong first, and every metric "verifiable from the
repository" are all facts about three repositories that are not this one.
Writing them without access is invention, which contributor policy §3
forbids, and a case study invented to fit the headings would be exactly the
marketing the ticket's Notes warn against.

To proceed the executor needs, per project, the maintainer's notes: the
problem, the approach, at least one thing that went wrong and what changed,
and each metric with where it was counted. A page of bullet points per
project is enough; the executor can write the prose and run the
proprietary-term scan. Alternatively, the maintainer writes the three files
and the executor works AC1, AC2 and AC4.
