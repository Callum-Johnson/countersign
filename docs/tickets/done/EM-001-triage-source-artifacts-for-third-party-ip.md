---
id: EM-001
title: Triage source artifacts for third-party IP before publication
status: done
tier: critical
complexity: M
dependencies: []
claimed_by: maintainer
claimed_at: 2026-08-31
closed_at: 2026-08-31
---

# EM-001 — Triage source artifacts for third-party IP before publication

> **Retrospective ticket.** This work was completed before the repository
> adopted its own process (ADR-0001). The ticket was written afterwards to
> record what was done and what was decided. It is not backdated: the git
> history shows the work landing in the initial commit, before this file
> existed. Recorded here because the decisions it contains are load-bearing
> for everything published.

## Context

The methodology this repository documents was developed on private projects,
two of which implement a ruleset owned by a third party. Nothing could be
published until every candidate artifact had been assessed for material that
is not mine to publish.

## Specification

Assess every architecture decision record and every closed ticket in the
source project against one test: does this artifact describe a third party's
intellectual property, or only my own engineering process?

Artifacts that cannot pass are excluded, not redacted.

## Acceptance criteria

1. AC1: Every ADR (39) and every closed ticket (292) is assessed. — **Met.**
   All 331 scored by an automated classifier.
2. AC2: Every artifact the classifier clears is then read manually. —
   **Met.** 29 cleared, 29 read.
3. AC3: Published artifacts contain no proprietary terms. — **Met.** Final
   repository-wide scan returns zero matches.
4. AC4: The method and its result are documented for the reader. — **Met.**
   `DISCLOSURE.md`.

## Out of scope

- Redacting artifacts to make them publishable. Excluded instead — a
  partially redacted document invites reconstruction of what was removed.
- Any source code from any project.

## References

- `DISCLOSURE.md`
- ADR-0001

## PR Description

### Ticket
EM-001 (retrospective)

### Tier
`critical` — publication decision affecting third-party rights. Independent
review not obtained; this work predates ADR-0002. Recorded as a gap rather
than reclassified.

### Summary
Two-pass triage of 331 artifacts. Ten published.

### Acceptance criteria
All four met; evidence inline above.

### How to verify
Run a proprietary-term scan across the repository; expect zero matches.
Compare `examples/` against the counts in `DISCLOSURE.md`.

### Risks / follow-ups
The classifier under-flagged: it cleared 22 tickets, of which manual review
rejected 15, including two containing domain terms inside code snippets that
scored below the two-occurrence threshold. **The classifier is not fit to be
relied on as written.** Raised as EM-001-001.
