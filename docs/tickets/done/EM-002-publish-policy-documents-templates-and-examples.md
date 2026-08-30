---
id: EM-002
title: Publish policy documents, templates and cleared examples
status: done
tier: standard
complexity: L
dependencies: [EM-001]
claimed_by: maintainer
claimed_at: 2026-08-31
closed_at: 2026-08-31
---

# EM-002 — Publish policy documents, templates and cleared examples

> **Retrospective ticket.** See the note on EM-001. Written after the work,
> not backdated.

## Context

With EM-001 establishing what could be published, the repository needed its
actual content: the policy documents describing the practice, the templates,
and the artifacts cleared for publication.

## Specification

Distil the working AI contributor policy, ticket lifecycle, tier review model,
quality gates and decision-record process into standalone documents that carry
no domain content. Copy the templates and cleared artifacts, normalising
project names and identifiers only.

## Acceptance criteria

1. AC1: Five policy documents exist under `docs/`. — **Met.**
2. AC2: Three templates exist under `templates/`, derived from the working
   versions rather than written fresh. — **Met.**
3. AC3: Cleared artifacts are published unmodified except for identifier
   normalisation, and the normalisation is disclosed. — **Met.**
   `DISCLOSURE.md`, "What is published".
4. AC4: Every internal link resolves. — **Met.** Link check clean.

## Out of scope

- Applying the documented process to this repository. Raised as EM-003.
- Per-project case studies beyond the growth summary. Raised as EM-004.

## References

- ADR-0001
- `DISCLOSURE.md`

## PR Description

### Ticket
EM-002 (retrospective)

### Tier
`standard` — new content, no existing contract altered.

### Summary
24 files, 2,540 lines: five policy documents, three templates, ten artifacts,
a growth case study, disclosure policy and licence.

### Acceptance criteria
All four met.

### How to verify
`find . -type f`; run the link check; confirm `templates/` against the source
project's originals.

### Risks / follow-ups
The repository documents a process it does not yet follow — the weakness
ADR-0001 addresses. Raised as EM-003.
