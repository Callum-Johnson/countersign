---
id: PRJ-XXX
title: <short imperative title>
status: ready          # ready | in-progress | blocked | done
tier: standard         # trivial | standard | critical
phase:                 # optional; a phase of the adopting project's own DESIGN.md, if it keeps one
complexity: M          # S (<1 day) | M (1-3 days) | L (3-7 days) | XL (split this)
dependencies: []       # list of ticket ids, e.g. [PRJ-001, PRJ-003]
claimed_by:            # filled when moved to active/
claimed_at:            # ISO date, filled when moved to active/
blocked_at:            # ISO date, filled when moved to blocked/
closed_at:             # ISO date, filled when moved to done/
---

# PRJ-XXX — <ticket title>

## Context

Why does this ticket exist? What is the problem it solves, or the
capability it adds? Two to four sentences. Link to the section(s) of
the adopting project's own DESIGN.md it advances.

## Specification

What exactly is being built. Be concrete. Include:

- File(s) to create or modify.
- Public types, functions, or APIs introduced.
- Data shapes (if any).
- Behaviour the code must exhibit.

This section is the contract. If you cannot describe the spec
concretely, the ticket is not ready and does not belong in `ready/`;
an adopting project may keep a fifth directory, `backlog/`, for such
tickets beyond the four `docs/ticket-lifecycle.md` documents.

### Files

- `core/foo/bar.py` — new module containing X
- `tests/unit/test_bar.py` — unit tests

### Public surface

```python
# Example signatures the ticket commits to
def thing(x: int, y: int) -> Thing: ...
```

### Behaviour

- Bullet list of behaviours the implementation must produce.
- Each bullet is independently verifiable.
- A ticket that adds a rule states the rule's falsifier here — the
  evidence that would retire it — per the tier review model, "Retiring a
  control". A rule-adding ticket without one is not ready.

## Acceptance criteria

Numbered, testable. Each one corresponds to a test or an inspectable
artefact. The PR description copies these and ticks them off with
evidence.

1. AC1: <specific testable claim>
2. AC2: <specific testable claim>
3. AC3: ...

## Out of scope

Explicit list of things this ticket does **not** include. Anything
listed here that the implementer does anyway is a PR rejection. If a
related concern is discovered during work, raise a new ticket and
reference it in the PR.

- Out of scope item 1
- Out of scope item 2

## References

- The adopting project's own DESIGN.md §X.Y, §X.Z
- External specification, by section identifier
- Other ticket IDs that established context
- ADR-NNNN if relevant

## Notes

Anything else the implementer should know that does not fit the above.
Optional. Examples: known tricky cases, recommended library, links to
prior conversations recorded as ADRs.

## PR Description

> Leave this section empty when authoring the ticket. The implementing
> agent fills it in before closing the ticket (move to `done/`).
> See `templates/PR-DESCRIPTION.md` for the required sub-section
> structure. A `PR.md` draft at the worktree root
> is allowed during implementation but is gitignored — the final copy
> lives here.

---

## Frontmatter `status:` values

The `status:` field is an enum with exactly these legal values, each
paired with the directory the ticket file must live in:

| `status:`     | Directory                 |
|---------------|---------------------------|
| `ready`       | `docs/tickets/ready/`     |
| `in-progress` | `docs/tickets/active/`    |
| `blocked`     | `docs/tickets/blocked/`   |
| `done`        | `docs/tickets/done/`      |

**Directory-status invariant:** the two are the same fact stored
twice and must always agree. Every move of a ticket file between
directories is paired with a frontmatter edit in the **same commit**:

- ready → active: set `status: in-progress`, `claimed_by`, `claimed_at`.
- active → blocked: set `status: blocked`, add `blocked_at`.
- active → done: set `status: done`, add `closed_at`.
- blocked → ready: set `status: ready`, clear `blocked_at`.

See `docs/ai-contributor-policy.md` and `docs/ticket-lifecycle.md`
("Claiming", "Closing") for the full procedures.

## How to use this template

1. Copy this file to `docs/tickets/ready/PRJ-XXX-<short-slug>.md` and give
   it an id, per `docs/ticket-lifecycle.md`, "Lineage" (the decision
   record is **ADR-0038**, in `examples/adr/`):

   - **Raised while working another ticket** (including by that ticket's
     second-agent review): append a three-digit sequence to the originating
     ticket's id — `PRJ-284-001`, then `PRJ-284-002`. A ticket raised while
     working *that* one is `PRJ-284-001-001`, and so on without limit. Find
     the next sequence by listing siblings of that one parent:
     `ls docs/tickets/*/PRJ-284-*`. Because the read is scoped to a single
     parent, two agents working different tickets cannot collide.
   - **Raised on its own account** — from a message from a downstream client, a
     rules audit, a planning pass, or the maintainer — continue the flat
     sequence: the highest flat `PRJ-NNN` across `ready/`, `active/`,
     `blocked/` and `done/`, plus one.

   The `id:` frontmatter carries the full lineage id and the filename repeats
   it. Lineage records **where a ticket came from, not what blocks it** — set
   `dependencies:` to whatever the ticket actually depends on, which may not
   include its parent.
2. Fill in every section. **Empty sections are not acceptable** — write
   `N/A` explicitly if a section genuinely does not apply (rare).
3. Set `tier` per the operative test in `docs/tier-review-model.md`.
4. Set `dependencies` to the list of ticket IDs that must be in `done/`
   before this can start.
5. Commit on a `docs/ticket-PRJ-XXX` branch (or directly to master if
   you have permission for trivial-tier ticket additions).

Every file the templates in this directory send a reader to exists in
this repository or is named, in those words, as the adopting project's
own; placeholder paths in the filled-in examples (`core/foo/bar.py`)
illustrate a form and send nobody anywhere.
**Retired when:** the templates are no longer published for copying, at
which point their references are internal to whoever holds them.

## Example: filled ticket

A fully-worked example lives at `examples/tickets/PRJ-001-repo-skeleton.md`.
Read it before writing your first ticket.
