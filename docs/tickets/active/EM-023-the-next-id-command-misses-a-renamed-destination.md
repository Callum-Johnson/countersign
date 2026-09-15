---
id: EM-023
title: The next-id command misses an id created by renaming a ticket file
status: in-progress
tier: standard
complexity: S
dependencies: []
claimed_by: claude-opus-5
claimed_at: 2026-09-15
---

# EM-023 — The next-id command misses a renamed destination

## Context

`docs/ticket-lifecycle.md`, "Lineage", says an id once created is spent, and
prescribes how to find the next one:

> Take the next number from the set of ticket files ever added — `git log
> --diff-filter=A --name-only --format= -- docs/tickets`, with the ids
> extracted from the paths — not from `ls`.

`--diff-filter=A` selects additions. An id created by **renaming** an existing
ticket file is recorded as a rename, not an addition, so its new id never
appears in that command's output. The rule protects against reusing an id
whose file was later removed; it does not protect against reusing an id that
arrived as a rename destination.

Measured on the control-plane project on 2026-09-08. `OMN-029` exists in
`docs/tickets/done/` on that repository's default branch, and was created by
renaming `OMN-028` after two agents allocated that identifier concurrently.
Against its history:

- `git log --all --diff-filter=A --name-only --format= -- docs/tickets/ | grep -oE "OMN-[0-9]{3}" | sort -u | tail -1` returns **OMN-028**.
- The same command with `--diff-filter=AR` returns **OMN-029**.
- Every id in the tree of every ref returns **OMN-029**.

So a contributor following the documented instruction on that repository would
have taken `OMN-029` as the next free identifier, and allocated an id already
in use — the exact failure the paragraph exists to prevent, reached by the one
route it does not cover.

This repository is not currently exposed: `EM-014-001` was created as an
addition rather than a rename, so the command sees it, and no EM id has
arrived by rename. The defect is in the published instruction, not in this
repository's history, and it reaches any project that adopts the rule and ever
renames a ticket file — which the same paragraph explicitly contemplates when
it says an id "raised and later deleted, absorbed or **renamed** leaves no
file".

## Specification

Documentation change only. The rule is unchanged; the command it prescribes is
corrected so that it answers the question the rule asks.

### Files

- `docs/ticket-lifecycle.md` — the "Lineage" paragraph's command
- `templates/TICKET.md` — its "How to use this template" step 1, if it repeats
  the command

### Public surface

The command is an instruction an adopter follows. Its output decides which
identifier they allocate, so a command that under-reports spent ids produces
collisions in the adopting project rather than in this one.

### Behaviour

- The prescribed command reports every id ever borne by a ticket file,
  including one that arrived as a rename destination. `--diff-filter=AR` is
  the minimal correction; a reader of every ref's tree is stronger and slower.
  Whichever is chosen, the paragraph says what it covers and what it does not.
- The paragraph states the case it now covers, so the next reader can see why
  the flag is what it is — the same way it already records the spent-id case
  that produced the original rule.
- The worked figures name the command that produced them and the repository
  and date they were taken at, per the contributor policy's §6.
- **This ticket adds no rule**, so it states no falsifier of its own; the
  existing rule's falsifier is unchanged.

## Acceptance criteria

1. AC1: the command in `docs/ticket-lifecycle.md`, run against a history in
   which a ticket file has been renamed to a new id, reports that id.
2. AC2: `templates/TICKET.md` and the lifecycle give the same command.
3. AC3: the paragraph states which allocation routes the command covers, and
   names the rename case as one of them.
4. AC4: no rule changes; the diff adds no `Retired when:` line and removes
   none.

## Out of scope

- The concurrent-allocation failure that produced `OMN-029` in the first
  place: two agents on refs neither could see, which no command over one
  repository's history can catch. That is a different defect with a different
  answer, and it belongs to whichever project meets it a second time.
- Renumbering any existing ticket.

## References

- `docs/ticket-lifecycle.md`, "Lineage" — the rule and the command
- `templates/TICKET.md`, "How to use this template" — where the command is
  repeated for an adopter
- The control-plane project's `OMN-029`, and the collision record in its own
  Notes, which is the measurement above

## Notes

Proposed `standard`: the change alters an instruction an adopter follows, and
under the operative test as it stands a process document that states no rule a
program executes is otherwise `trivial`. The tier question EM-007-002 owns
applies here as it does to every documentation ticket on this board; the
executor may raise and never lower, so the higher tier is the one an author
can propose without resolving it.

## PR Description

> Leave this section empty when authoring the ticket.
