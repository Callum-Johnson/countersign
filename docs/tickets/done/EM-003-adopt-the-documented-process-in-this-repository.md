---
id: EM-003
title: Adopt the documented process in this repository
status: done
tier: critical
complexity: S
dependencies: [EM-002]
claimed_by: maintainer
claimed_at: 2026-08-31
closed_at: 2026-08-31
---

# EM-003 — Adopt the documented process in this repository

## Context

The repository documents a ticket lifecycle, a tier model and an agent policy,
and asserts they were applied continuously to a private project. Its own
history shows the initial commit landing 2,540 lines with no ticket and no
decision record.

That gap is the first thing a sceptical reader checks, and it is fair. See
ADR-0001 for the reasoning and the rejected alternative of backdating.

## Specification

Create the decision-record and ticket directories described in
`docs/ticket-lifecycle.md`, populate them with the real decisions and real
work, and link the board from the README.

### Files

- `docs/adr/` — ADR-0001, ADR-0002
- `docs/tickets/{ready,active,blocked,done}/` — the current board
- `docs/tickets/README.md` — pointer to the template
- `README.md` — link to the board

### Behaviour

- Directory and `status:` frontmatter agree for every ticket.
- Retrospective tickets are labelled as such in their body.
- No ticket is dated earlier than the commit that introduces it.

## Acceptance criteria

1. AC1: `docs/adr/` contains the adoption decision and the single-maintainer
   review decision.
2. AC2: All four ticket directories exist, with the board populated.
3. AC3: Every ticket's directory matches its `status:` field.
4. AC4: Retrospective tickets state plainly that they were written after the
   work.
5. AC5: No ticket claims a date earlier than its introducing commit.
6. AC6: The README links the board.

## Out of scope

- Rewriting git history to insert tickets before the initial commit.
- Per-project case studies (EM-004).
- Publication (EM-005).

## References

- ADR-0001, ADR-0002
- `docs/ticket-lifecycle.md`

## PR Description

### Ticket
EM-003

### Tier
`critical` — process-surface change (clause 5 of the operative test): it
establishes how work on this repository is governed.

**Independent review not obtained.** Per ADR-0002 this is recorded rather than
worked around, and the tier is not reclassified to avoid it. The verification
below was performed by the executor, which is not the same thing.

### Summary
Created `docs/adr/` and the four ticket directories, populated the board with
two retrospective tickets, one active, one blocked and two ready, added
ADR-0001 and ADR-0002, and linked the board from the README.

### Acceptance criteria
1. AC1 — met. `docs/adr/` contains ADR-0001 (adoption) and ADR-0002
   (single-maintainer review).
2. AC2 — met. All four directories exist; board has six tickets.
3. AC3 — met. Invariant check across all six passes: every `status:` field
   matches its directory.
4. AC4 — met. EM-001 and EM-002 both open with a labelled retrospective note.
5. AC5 — met. No ticket carries a date earlier than the commit introducing it;
   all are dated 2026-08-31 and land in this commit.
6. AC6 — met. README links the board, both ADRs, and states the gap plainly.

### Out of scope
Confirmed: no git history was rewritten, no case studies added (EM-004), no
publication attempted (EM-005).

### How to verify
Run the directory/status invariant check over `docs/tickets/*/`. Compare
ticket dates against `git log --format='%ad %s'`. Confirm the README's claim
about the initial commit by inspecting the first commit's file list.

### Risks / follow-ups
- The repository still cannot satisfy its own critical-review requirement.
  ADR-0002 documents the substitute; this PR is itself an instance of the gap.
- The triage that gates all published content is not yet reproducible
  (EM-001-001).
