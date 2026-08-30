# Ticket lifecycle

Work is defined in ticket files that live in the repository and move between
directories as their state changes.

```
docs/tickets/
├── TEMPLATE.md
├── ready/       specified, dependencies met, available to claim
├── active/      claimed, in progress, one owner
├── blocked/     cannot proceed; carries a BLOCKER: comment
└── done/        merged, with the PR description appended
```

## The directory/status invariant

Every ticket carries a `status:` field in its frontmatter **and** sits in the
directory matching it. The two are the same fact stored twice, and they must
always agree.

| `status:` | Directory |
|---|---|
| `ready` | `ready/` |
| `in-progress` | `active/` |
| `blocked` | `blocked/` |
| `done` | `done/` |

Every move pairs the file move and the frontmatter edit **in a single commit**.

Storing the same fact twice is normally a smell. Here it is the point: the
redundancy is a continuous integrity check that costs nothing to maintain and
makes drift visible. A ticket whose field and directory disagree is a
workflow error you can find with a script, and a contributor that half-completed
a transition leaves evidence rather than a silent inconsistency.

## Claiming

1. Branch, with a name beginning with the ticket identifier.
2. Move the file from `ready/` to `active/`.
3. Set `status: in-progress`, `claimed_by`, `claimed_at`.
4. Commit: `chore(PRJ-XXX): claim ticket`.

If two agents race for the same ticket, the second move produces a merge
conflict on the next pull. **Lose gracefully**: drop the branch, take a
different ticket.

That is deliberately a crude lock. It costs one wasted claim commit, requires
no coordination service, and cannot fail in a way that silently permits two
agents to work the same ticket — which is the failure that actually matters.

## Blocking

An agent that cannot proceed adds a comment prefixed `BLOCKER:` stating what
is unclear and what it would need, commits it, moves the ticket to `blocked/`,
and picks up something else.

Blocking is a **success path**, not a failure. An agent that blocks has
correctly identified that it does not have enough information — which is
precisely the judgement that is hardest to elicit, and the alternative is an
invented interpretation that looks like progress.

## Closing

1. Append the pull-request description to the ticket file — ticket, tier,
   summary, each acceptance criterion ticked with evidence, out-of-scope
   confirmation, verification steps, risks and follow-ups.
2. Move to `done/`, set `status: done` and `closed_at`.
3. Commit: `chore(PRJ-XXX): close ticket`.

The description lives in the ticket file, not only in a code-forge interface.
The repository has to remain the record: forge metadata is not portable, not
greppable offline, and not guaranteed to outlive the host.

## Lineage

Work discovered mid-ticket becomes a new ticket numbered as a child of its
origin: a ticket raised while working `PRJ-284` is `PRJ-284-001`, and one
raised while working that is `PRJ-284-001-001`, without limit.

Lineage records **where a ticket came from, not what blocks it** — dependencies
are declared separately and often do not include the parent.

The scheme has a practical property: finding the next number means listing the
siblings of one parent, so two agents working different tickets cannot collide
on identifiers. It also means every ticket answers "why does this exist?"
without anyone having to remember.
