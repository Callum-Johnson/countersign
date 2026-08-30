---
id: PRJ-012
title: Flip ticket frontmatter status to "done" on close
status: done
tier: trivial
phase: 1
complexity: S
dependencies: []
claimed_by: agent-str-012
claimed_at: 2026-06-30
closed_at: 2026-06-30
---

# PRJ-012 — Flip ticket frontmatter status to "done" on close

## Context

PRJ-001, PRJ-002, and PRJ-004 all landed with their frontmatter
`status:` still reading `in-progress` even after being moved to
`docs/tickets/done/`. The directory was the source of truth, but
the frontmatter contradicted it. Anything that filters tickets by
status (UI, scripts) would get the wrong answer.

The procedure in AGENTS.md does not explicitly require flipping
`status:` on close. Add the step.

## Specification

### Files

- `AGENTS.md` — claim/close procedure.
- `CONTRIBUTING.md` — §6 (merging) and §7 (blockers).
- `docs/tickets/TEMPLATE.md` — frontmatter description.
- `docs/tickets/done/PRJ-001-repo-skeleton.md`
- `docs/tickets/done/PRJ-002-core-ids-and-primitives.md`
- `docs/tickets/done/PRJ-004-dice-engine.md`
- (Any other `done/` tickets at time of execution.)

### Workflow change

The close commit must include both:
1. `git mv docs/tickets/active/PRJ-XXX-*.md docs/tickets/done/`
2. Edit the frontmatter: set `status: done`, add `closed_at: <ISO date>`.

Same for blocking: the block commit must set `status: blocked` and
add `blocked_at: <ISO date>`.

### Status enum

The legal values for `status:` are now exactly:
- `ready` (in `docs/tickets/ready/`)
- `in-progress` (in `docs/tickets/active/`)
- `blocked` (in `docs/tickets/blocked/`)
- `done` (in `docs/tickets/done/`)

Document in TEMPLATE.md. The directory and the status must agree.

### Backfill

Open all existing `done/` ticket files and set `status: done` and
add `closed_at: 2026-06-30` (today). Single commit:
`chore(PRJ-012): backfill status: done on existing closed tickets`.

## Acceptance criteria

1. AGENTS.md "Ticket claim procedure" updated to include the
   frontmatter flip on close.
2. CONTRIBUTING.md §6 (merging) updated to require the frontmatter
   flip in the close commit.
3. CONTRIBUTING.md §7 (blockers) updated to include
   `status: blocked` + `blocked_at`.
4. `docs/tickets/TEMPLATE.md` documents the legal `status:` values
   and the directory-status invariant.
5. All existing `done/` ticket files have `status: done` and
   `closed_at`.
6. `bash ci/run-checks.sh` passes.

## Out of scope

- Adding tooling to enforce the directory-status invariant
  (a linter). Optional future ticket.
- Renaming the directories. They stay as-is.

## References

- AGENTS.md "Ticket claim procedure" section.
- CONTRIBUTING.md §6 and §7.
- `docs/tickets/TEMPLATE.md`.

## Notes

`tier: trivial` — pure docs + small edits to existing markdown
files.

## PR Description

### Ticket
PRJ-012 — Flip ticket frontmatter status to "done" on close

### Tier
trivial

### Summary
Closes a workflow gap: every ticket file in `docs/tickets/done/`
prior to PRJ-011 still carried `status: in-progress` in its
frontmatter, contradicting its directory location. The four
workflow docs are updated to require flipping `status:` on every
move between ticket directories (claim, close, block, unblock),
and `closed_at` / `blocked_at` ISO-date fields are introduced.
All seven existing closed tickets are backfilled in one commit so
the directory and the `status:` field now agree everywhere.

### Acceptance criteria
- [x] AC1: AGENTS.md "Ticket claim procedure" updated to include
  the frontmatter flip on close. Evidence: AGENTS.md gained a new
  "How to close a ticket" subsection (commit `7ca7e96`) right
  after "How to claim a ticket", spelling out the three-step
  close procedure (`git mv` to `done/`, set `status: done` +
  `closed_at`, commit as `chore(PRJ-XXX): close ticket`) and a
  pointer to the directory-status invariant in TEMPLATE.md.
- [x] AC2: CONTRIBUTING.md §6 (merging) updated to require the
  frontmatter flip in the close commit. Evidence: §6 rewritten
  (commit `7ca7e96`) so the close-commit bullet now enumerates
  three sub-steps — `git mv` then frontmatter edit
  (`status: done` + `closed_at`) then commit — and a trailing
  paragraph names the directory/`status:` invariant explicitly.
- [x] AC3: CONTRIBUTING.md §7 (blockers) updated to include
  `status: blocked` + `blocked_at`. Evidence: §7 procedure
  expanded from four to five steps (commit `7ca7e96`): the
  `git mv` step is now explicitly prefixed, a new step sets
  `status: blocked` and adds `blocked_at`, and the
  resolution paragraph adds the reverse flip back to
  `status: ready` when unblocking.
- [x] AC4: `docs/tickets/TEMPLATE.md` documents the legal
  `status:` values and the directory-status invariant. Evidence:
  TEMPLATE.md (commit `7ca7e96`) adds `blocked_at:` and
  `closed_at:` to the frontmatter example, plus a new
  "Frontmatter `status:` values" section with a
  status-to-directory table and the four directory-transition
  rules naming the exact frontmatter edits each requires.
- [x] AC5: All existing `done/` ticket files have `status: done`
  and `closed_at`. Evidence: single backfill commit `e43d106`
  touches all seven files under `docs/tickets/done/` —
  PRJ-001, PRJ-002, PRJ-003, PRJ-004, PRJ-005, PRJ-006 flip
  `status: in-progress` → `status: done`, and all seven gain
  `closed_at: 2026-06-30`. PRJ-011 already had `status: done`
  (the only file that did), so it only gained `closed_at`. This
  ticket's own file gains `status: done` + `closed_at` in the
  close commit per the new procedure.
- [x] AC6: `bash ci/run-checks.sh` passes. Evidence: full local
  run completed with `==> all checks passed` — ruff check
  clean, ruff format --check clean (24 files), mypy --strict
  clean (10 source files), pytest 196 passed.

### Out of scope (per ticket)
Confirm nothing in this PR exceeds the ticket's scope:
- No tooling / linter to enforce the directory-status
  invariant. The ticket explicitly defers this as an optional
  future ticket; for now the invariant is documented prose.
- No directory renames. The four directories (`ready`, `active`,
  `blocked`, `done`) keep their existing names.
- No edits to code under `core/`, `content/`, or `tests/`. No
  edits to DESIGN.md or `docs/conventions.md`. No edits to
  other ready/active/blocked ticket files — only the seven
  `done/` files for backfill, plus this ticket file.

### How to verify
1. `bash ci/run-checks.sh` from the worktree root — must exit 0.
2. `head -11 docs/tickets/done/PRJ-*.md` — every closed ticket
   shows `status: done` and a `closed_at:` line.
3. `grep -n "closed_at\|blocked_at" docs/tickets/TEMPLATE.md
   AGENTS.md CONTRIBUTING.md` — the two new fields are
   referenced in all three workflow docs.
4. `grep -n "How to close a ticket" AGENTS.md` — the new
   subsection exists immediately after "How to claim a ticket".
5. `git log --oneline PRJ-012-frontmatter-status` — four
   commits: claim, docs change, backfill, close.

### Risks / follow-ups
- The invariant is enforced by author discipline, not by CI.
  A small linter that checks every file under each ticket
  directory has the matching `status:` would close the loop;
  noted as optional future work in the ticket spec.
- The `blocked_at` and `closed_at` fields are additive — any
  existing tooling that reads ticket frontmatter (none today)
  must tolerate the new keys.
- No tickets currently live under `docs/tickets/blocked/`, so
  the blocker-procedure changes are documented but not
  exercised against existing files in this PR.
