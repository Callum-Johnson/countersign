# ADR-0038: A ticket raised while working another ticket carries that ticket's id

- **Status:** accepted
- **Date:** 2026-08-28
- **Deciders:** engine maintainer
- **Related:** `docs/tickets/TEMPLATE.md` (the numbering procedure this
  changes), AGENTS.md ("What to do when blocked"), CONTRIBUTING.md §7
  (out-of-scope discovery), ADR-0007 (tiering, unchanged by this)

## Context

Ticket ids were a flat sequence: take the highest existing number across
`ready/`, `active/`, `blocked/` and `done/`, and add one. That worked while
one agent worked one ticket at a time. It stopped working the moment several
ran concurrently.

Two costs, both paid repeatedly:

1. **Collisions.** Four agents each told to "take the next free number" take
   the *same* number, because each reads the tree before any of them writes.
   This happened three times in one batch, and again in the batch after it,
   each time needing a manual renumber and a sweep of every reference across
   ticket prose, code comments and tests. Reserving a private range per agent
   fixed the collisions but not the second cost.

2. **Lost provenance.** A flat id says nothing about why the ticket exists.
   `PRJ-273` reads as the 273rd idea somebody had; it was in fact found by
   the second-agent review of `PRJ-257`, and that lineage is the single most
   useful thing to know when triaging it. The provenance existed only in
   prose, where it went stale or was never written.

## Decision

**A ticket raised while working another ticket is numbered by appending a
three-digit sequence to the originating ticket's id**, separated by a hyphen:

```
PRJ-900            a ticket raised on its own account   (a hypothetical id;
                                                        no such ticket exists)
PRJ-900-001        the first ticket raised while working PRJ-900
PRJ-900-002        the second
PRJ-900-001-001    a ticket raised while working PRJ-900-001
```

Nesting is unbounded; each level appends its own `-NNN`.

### What counts as "while working"

The originating ticket is the one whose work surfaced the issue -- including
work done by that ticket's **second-agent review**, which is part of the same
ticket's lifecycle. A review of `PRJ-900` that finds a defect raises
`PRJ-900-00N`, not a ticket of its own lineage.

### What keeps a flat id

A ticket that does not arise from another ticket's work: one seeded from a
`client/to-engine/` message, from a rules audit, from a planning pass, or
by the maintainer directly. These continue the flat `PRJ-NNN` sequence.

### Mechanics

- The sequence is **per parent** and starts at `001`. To find the next one,
  list siblings: `ls docs/tickets/*/PRJ-900-*` -- a read scoped to one
  parent, which is why two agents working *different* parents cannot
  collide.
- The `id:` frontmatter carries the full lineage id, and the filename is
  `PRJ-900-001-<short-slug>.md`. The directory/status invariant is unchanged.
- `dependencies:` still names whatever the ticket actually depends on. A
  child is **not** automatically dependent on its parent -- lineage records
  where it came from, not what blocks it.
- Tiering is unaffected: a child is tiered on its own change by the ADR-0007
  operative test, exactly as any other ticket.

## Consequences

**Collisions become structurally impossible between agents working different
tickets**, which is the case that kept biting. Two agents working the *same*
parent can still collide on `-001`; the coordinator assigns those, as it did
with reserved ranges, but that is now a rare case rather than the default.

**Provenance is in the id**, so `ls docs/tickets/ready/` shows lineage without
opening a file, and children sort adjacent to their parent.

**Ids get longer**, and a deep chain (`PRJ-900-001-001`) is a signal worth
reading: it means a fix raised a fix that raised a fix. If a lineage runs
deep, the root ticket probably under-scoped its problem.

**Existing flat ids are not renumbered.** Every ticket in `done/` keeps the id
it shipped under, and every reference to it in an ADR, a commit message, a
`client/` message or a code comment stays correct. This convention applies
to tickets raised from here on.

## Alternatives considered

**Keep flat ids, keep reserving ranges per agent.** Works for collisions,
which is why it was used, but it is coordinator bookkeeping that has to be got
right every batch, and it does nothing for provenance. Rejected because the
failure mode is silent: a coordinator who forgets to reserve gets a collision
discovered at merge.

**A central counter file.** Would need locking to be correct under concurrency,
and a lock in a git tree is a worse problem than the one it solves.

**Record provenance in frontmatter (`raised_by:`) and keep flat ids.** Honest
and simple, and it was close. Rejected because the id is what appears in
commit messages, branch names, code comments and client messages -- the places
a reader meets a ticket without its file to hand. Putting lineage in the id
puts it everywhere the id already goes.

---

## Annotation — added 2026-09-06 under EM-006

> This section is not part of the decision as recorded. Everything above the
> horizontal line is the original text. It is added in place rather than by superseding
> the record because the decision is sound and its operating instructions are
> incomplete; a reader copying the scheme needs the correction beside it.

The scheme's lookup instruction reads a smaller set than the set an id must be
unique in. That is one defect with two faces.

**1. The same id under two slugs merges silently.** The id lives in the
filename and the frontmatter, and git compares paths. `PRJ-900-001-first.md`
in the main tree and `PRJ-900-001-second.md` on a branch are two files for one
id, and the branch merges with no conflict. The sibling listing above then
shows two `-001`s: two agents can claim one ticket from different files, and
the count of siblings no longer says how many tickets there are. The
mechanism is structural and can be reproduced on demand; it needs no race.

*Placement rule:* a ticket raised by a second-agent review of a branch is
created **on that branch**, not in the main tree — by the executor, from the
review's record, since the reviewer does not write to the tree it reviews. The sibling listing the next
id is read from is then the listing the id will land in, and a duplicate
becomes a path conflict at merge — the same crude lock claiming relies on —
instead of a silent second file.

**2. An id, once created, is spent, and the tree does not know it.** "The
highest across the ticket directories" reads the working tree. A ticket
raised and later deleted, absorbed or renamed leaves no file behind and
remains named in closed tickets, commit messages and pull-request bodies. On
the project this record comes from, measured against its default branch when
EM-006 was raised, fourteen ids had been created and later had their file
removed, and the next flat id was taken, worked and closed before anyone
noticed it had been used before — the fourteenth. (On the branch that found
it the count is thirteen, because there the reused id has a file again.)

*Next-id rule:* the next id comes from **history**, not the tree — the set of
ticket files ever added:

```sh
git log --diff-filter=A --name-only --format= -- docs/tickets \
  | sed -nE 's#.*/(PRJ-[0-9]+(-[0-9]+)*)-.*#\1#p' | sort -u
```

A reused id is not renumbered after the fact, consistent with the
no-retroactive-renumbering rule above. The newer ticket records the reuse and
points at the older use.
