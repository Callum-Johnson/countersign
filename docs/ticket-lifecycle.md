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

**Retired when:** a tool derives one of the two from the other at every move and the second copy cannot disagree; the check then checks nothing.

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

**Retired when:** two agents are shown to have worked the same ticket without a conflict — the lock failed silently, which it is designed not to do — or the project adopts a coordination service that makes the file move redundant.

## Blocking

An agent that cannot proceed adds a comment prefixed `BLOCKER:` stating what
is unclear and what it would need, commits it, moves the ticket to `blocked/`,
and picks up something else.

Blocking is a **success path**, not a failure. An agent that blocks has
correctly identified that it does not have enough information — which is
precisely the judgement that is hardest to elicit, and the alternative is an
invented interpretation that looks like progress.

*Falsifier:* stated with the rule in the contributor policy's §3 and not restated here.

## Closing

1. Append the pull-request description to the ticket file — ticket, tier,
   summary, each acceptance criterion ticked with evidence, out-of-scope
   confirmation, verification steps, risks and follow-ups.
2. Move to `done/`, set `status: done` and `closed_at`.
3. Commit: `chore(PRJ-XXX): close ticket`.

The description lives in the ticket file, not only in a code-forge interface.
The repository has to remain the record: forge metadata is not portable, not
greppable offline, and not guaranteed to outlive the host.

**Retired when:** the forge's metadata is exported into the repository automatically on every close, so the description is in the record without being appended.

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

**Retired when:** lineage reaches a depth the project's tooling cannot carry, or provenance is recorded in frontmatter and read in every place the id appears — commit messages, branch names, comments — which ADR-0038 rejected because it is not.

Three things the scheme does not say for itself, each found in use:

**A ticket raised by a review is created on the branch under review** — by
the executor, from the review's record, before the next round or the close;
the reviewer names the ticket and the executor writes it, so that the
reviewer need not write to the tree it reviews. The id lives in the filename
and git compares paths, so one id written under two
slugs in two places — a review's copy in the main tree, the executor's on the
branch — is two files for one id, and it merges with no conflict. Nothing in
the scheme detects it, and two agents can then claim one ticket from different
files. Creating the ticket where the review is means the sibling listing that
yields the next id is the listing the id will land in, and a duplicate becomes
a merge conflict, which is the crude lock this lifecycle already relies on,
rather than a silent second file.

**Retired when:** the merge tool compares ids rather than paths — a merge driver that conflicts on a duplicate id under any slug — so that placement no longer decides whether a collision is seen.

**The next id comes from history, not the tree.** An id, once created, is
spent. A ticket raised and later deleted, absorbed or renamed leaves no file
and remains named in closed tickets, commit messages and pull-request bodies,
and a read of the tree hands its id out again. Take the next number from the
set of ticket files ever added — `git log --diff-filter=A --name-only
--format= -- docs/tickets`, with the ids extracted from the paths — not from
`ls`. This repository already has one such id:
`EM-010-001` was created at 3da6c57 and renamed `EM-014-001` at 0947dda, so
the tree shows no child of EM-010 while the history does, and the next child
of EM-010 read from the tree would be `-001` again. On the source project — the
rules engine in the growth case study — the count stood at fourteen against
its default branch when EM-006 was raised, and
the fourteenth was taken, worked and closed before anyone noticed. A reused id
is not renumbered afterwards; the newer ticket records the reuse and points at
the older use.

**Retired when:** the project forbids deleting a ticket file — tickets are only ever moved — so that the tree is the history and reads the same.

**A fixed commit-subject length does not compose with lineage ids.** No
subject-length rule is published here. A project that brings one should
choose, because a fourth-generation id such as `PRJ-284-001-001-001` takes
roughly a third of a 72-character subject before the verb, and on the source
project a 72-character limit was breached routinely once lineage ran deep,
including by merge commits on the default branch. Two conventions that cannot
both be followed are worse than either alone: the one enforced by nothing is
the one dropped, and it is dropped silently. Exempt the id prefix from the
count, or drop the limit, but decide.


*Not a rule.* This paragraph states a hazard and refuses no convention; it carries no falsifier.