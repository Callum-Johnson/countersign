---
id: PRJ-011
title: Remove PR.md from repo root workflow
status: done
tier: trivial
phase: 1
complexity: S
dependencies: []
claimed_by: agent-str-011
claimed_at: 2026-06-30
closed_at: 2026-06-30
---

# PRJ-011 — Remove PR.md from repo root workflow

## Context

Surfaced during wave 2 of Phase 1 implementation. Every ticket
branch wrote a `PR.md` at the repo root per CONTRIBUTING.md §3.
When two branches landed in parallel (PRJ-002 and PRJ-004), the file
produced a merge conflict because each branch had overwritten the
previous content. Dead PR text from completed tickets was
accumulating on master.

The PR description is useful as a review artefact but should not
live at the repo root post-merge.

## Specification

### Files

- `CONTRIBUTING.md` — update §3.
- `AGENTS.md` — update any references to PR.md.
- `docs/tickets/TEMPLATE.md` — note new convention.
- Delete `PR.md` from repo root if still present.
- Add `PR.md` to `.gitignore`.

### Workflow change

The PR description goes **into the ticket file** under a new
`## PR Description` section that the agent writes when closing the
ticket. The file is moved from `active/` to `done/` with this
section appended.

This means:
- No file at repo root at any time.
- The full review trail lives with the ticket in `done/PRJ-XXX-*.md`.
- No merge conflicts.
- Grep-friendly: `grep -A 50 "PR Description" docs/tickets/done/PRJ-XXX-*.md`.

Update the CONTRIBUTING.md §3 template to be a markdown section
template that fits inside the ticket file rather than a standalone
file template.

### PR.md still allowed as a working draft

Agents may write `PR.md` at the worktree root **as a working draft
during implementation**, but it must be added to `.gitignore` and
**must not be committed**. The final version is appended to the
ticket file before close.

### Backfill: forward-fix only

The five existing closed tickets (PRJ-001, PRJ-002, PRJ-003, PRJ-004,
PRJ-005) had their PR descriptions written as ephemeral PR.md files
that were deleted on merge to resolve conflicts. Their full text
remains retrievable via `git show <commit>:PR.md` against the
`docs(PRJ-XXX): add PR description` commits on each merged branch.
This ticket does **not** backfill them — the cost outweighs the
value, the information lives in git history, and the agent return
reports are also archived. New tickets from PRJ-006 onward use the
new convention.

## Acceptance criteria

1. CONTRIBUTING.md §3 updated: PR description goes in the ticket
   file's `## PR Description` section, not a separate file.
2. AGENTS.md updated to match (any references to PR.md adjusted).
3. `docs/tickets/TEMPLATE.md` updated to reflect the new structure.
4. `PR.md` added to `.gitignore`.
5. `bash ci/run-checks.sh` passes.

## Out of scope

- Changing the PR description template content itself — same
  required sections.
- Tooling automation (a script that builds a PR doc from commit
  messages). Optional future ticket.

## References

- CONTRIBUTING.md §3.
- Original workflow conversation captured in `docs/adr/` if created;
  otherwise this ticket is the record.

## Notes

This is `tier: trivial` because it is purely docs + small file
moves. No tests touched.

## PR Description

### Ticket
PRJ-011 — Remove PR.md from repo root workflow

### Tier
trivial

### Summary
Replaces the root-level `PR.md` PR-description convention with a
`## PR Description` section appended to the ticket file before
close. Eliminates the merge-conflict pattern that surfaced when
parallel branches each overwrote `PR.md`, and keeps the review
trail attached to the ticket forever. `PR.md` at the worktree root
is now allowed as a working draft only — it is gitignored and must
not be committed. This ticket's own PR description is the new
convention's first example.

### Acceptance criteria
- [x] AC1: CONTRIBUTING.md §3 updated — PR description goes in the
  ticket file's `## PR Description` section, not a separate file.
  Evidence: `CONTRIBUTING.md` §3 rewritten (commit `ab8398b`); the
  template is now framed as a markdown section appended to the
  ticket file, and the standalone-`PR.md` language is removed.
  §6 (Merging) updated to match.
- [x] AC2: AGENTS.md updated to match — any references to PR.md
  adjusted. Evidence: `AGENTS.md` "What 'done' looks like" section
  updated (commit `ab8398b`) to point at the in-ticket-file
  `## PR Description` section and to note that a root-level
  `PR.md` is allowed as a gitignored working draft only.
- [x] AC3: `docs/tickets/TEMPLATE.md` updated to reflect the new
  structure. Evidence: a placeholder `## PR Description` section
  with a usage note was added to the template (commit `7c9a338`)
  so future ticket authors see the expected shape; the section
  defers to CONTRIBUTING.md §3 for the sub-section list.
- [x] AC4: `PR.md` added to `.gitignore`. Evidence: both `PR.md`
  and `/PR.md` patterns added to `.gitignore` under a new
  comment block (commit `d7a65a6`).
- [x] AC5: `bash ci/run-checks.sh` passes. Evidence: full run
  completed locally with `==> all checks passed` — ruff check
  clean, ruff format --check clean (22 files), mypy --strict
  clean (9 source files), pytest 173 passed.

### Out of scope (per ticket)
Confirm nothing in this PR exceeds the ticket's scope:
- No backfill of PR descriptions into existing `done/` tickets
  (PRJ-001 through PRJ-005). The ticket explicitly drops that AC;
  prior PR text remains retrievable via `git show <commit>:PR.md`
  on the merged branches.
- No template-content changes — same required sub-sections, only
  the container and section-header depth changed.
- No automation tooling (a script that drafts a PR section from
  commit messages). Listed as an optional future ticket in PRJ-011.
- No code, tests, DESIGN.md, or other ticket files touched.

### How to verify
1. `bash ci/run-checks.sh` from the worktree root — must exit 0.
2. `grep -n "PR Description" CONTRIBUTING.md docs/tickets/TEMPLATE.md`
   — both files reference the new section.
3. `grep -n "PR.md" AGENTS.md CONTRIBUTING.md .gitignore` — the
   only mentions are: the gitignore patterns, and prose framing
   `PR.md` as a gitignored working draft (not as a deliverable).
4. `git log --oneline PRJ-011-pr-md-workflow-fix` — five commits:
   claim, docs change, template change, gitignore change, close.
5. This very ticket file under `docs/tickets/done/` exemplifies
   the new convention: read this `## PR Description` section as
   the reference example.

### Risks / follow-ups
- No code paths changed, so runtime risk is nil.
- Workflow risk: agents in flight on other branches (e.g. PRJ-006)
  were briefed on the old convention. They may still write a
  root-level `PR.md`; because `PR.md` is now gitignored, an
  accidental `git add PR.md` will be silently skipped and the
  draft will not enter master. The agent must remember to append
  the final copy to its ticket file before close — this is now
  documented in CONTRIBUTING.md §3, §6, and AGENTS.md.
- No follow-up tickets created. The optional automation tooling
  mentioned in the ticket's Out of Scope is deferred indefinitely.
