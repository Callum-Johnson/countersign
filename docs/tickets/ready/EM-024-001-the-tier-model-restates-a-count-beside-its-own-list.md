---
id: EM-024-001
title: The tier model restates a count beside its own list
status: ready
tier: standard
complexity: S
dependencies: [EM-024]
---

# EM-024-001 — The tier model restates a count beside its own list

## Context

EM-024 lands `docs/quality-gates.md`, "A count that describes the tree has one
site that goes red", which asks that a count describing the tree have one site,
that the site be one that fails when the tree moves, and that every other
mention name the site rather than the number. The first thing that section
binds is this repository, and `docs/tier-review-model.md` carries two
non-complying sentences, in two different sections, both of which state
"thirteen".

**The first**, in "Retiring a control", in the paragraph beginning "**A rule
needs a second instance**", reads: "Of the thirteen rule-adding tickets from
EM-006 to EM-020, eight name one source ticket on one project in their
Context — EM-007, EM-008, EM-010, EM-011, EM-012, EM-012-001, EM-014-001 and
EM-019-001 — counted by reading each Context for the source it names." Two
counts, two defects, one sentence:

- **"eight" is restated beside its own list.** The enumeration that follows it
  is the site. The number is a second copy of what the list already says, and
  the two can disagree the moment a ticket is added to or removed from the
  list — which is exactly the shape EM-024's Context records four times over.
- **"thirteen" has no site at all.** No list, no command, no test. It is the
  kind of number EM-024 was raised about: a reader who doubts it must
  reconstruct the population "rule-adding tickets from EM-006 to EM-020" by
  hand, which is the work the sentence's own closing clause admits to.

**The second**, in "When review ends", in the Retired-when line of the
paragraph beginning "**The repair is read whole**", reads: "At 5d94db7, before
the rule, the count was five, over the thirteen closed tickets that carry a
Review table." It names a baseline and no site, and the population it counts
has moved since that baseline while the sentence has not:
`git grep -l "| Round | Must-fix |" 5d94db7 -- docs/tickets/done | wc -l`
returns 13, and the same command at `60f39fb`, the last commit that changes
`docs/tickets/done/`, returns 16. Nothing goes red on the difference, and its
present tense — "that carry" — reads as a claim about the tree now. It is the
same defect as the first and in the same document, which is why it is folded
in here rather than raised separately; a repair that fixed one and left the
other standing would be the duplication failure the section is about.

Found on 2026-09-08 while working EM-024 — the first by reading the document
the new section binds, the second at the round-1 independent review of EM-024,
which recorded it as a must-fix against this ticket for leaving a sibling
unraised. Both are located by `grep -n "thirteen" docs/tier-review-model.md`,
which at `de99c4e`, the last commit that changes that file, returns lines 374
and 489. The earlier, narrower command recorded here,
`grep -n "thirteen rule-adding" docs/tier-review-model.md`, returned nothing:
the phrase wraps, "thirteen" ending line 489 and "rule-adding" beginning line
490. A grep is line-oriented and a phrase that wraps is invisible to it. That
is a property of the instrument and not of this repository's prose, and it is
worth stating here because a ticket about numbers a reader cannot check should
not carry a command that does not run.

## Specification

Both sentences keep their evidence and lose their unpinned numbers. Three
changes, independently decidable by the executor:

- The enumeration stays and "eight" goes, or "eight" stays and the enumeration
  moves to a site the sentence points at. The first is the cheaper reading and
  is what OMN-024's round 3 chose for its own sibling list; the ticket does not
  mandate it.
- The first "thirteen" either gains, in the same sentence, the command that
  produces it with its baseline — the population is a range of ticket ids, so a
  command over `git log --diff-filter=A --name-only --format= -- docs/tickets`
  can be written — or the sentence drops the count and names the range it
  already names, letting the reader count if the reader cares.
- The second "thirteen", in "When review ends", takes the same treatment. It
  already names a baseline, so the cheaper repair is the command:
  `git grep -l "| Round | Must-fix |" 5d94db7 -- docs/tickets/done | wc -l`
  produces it and is the site. The alternative is to drop the population from
  the sentence, which loses nothing the falsifier needs — "five must-fixes, all
  of them inside the previous round's repair" carries the argument without the
  denominator. Whichever is chosen, the tense stops reading as a claim about
  the tree now.

Nothing else in either paragraph changes. The rules those paragraphs state —
the second-instance bar, and the read-whole obligation with its falsifier —
are not touched; these are their evidence sentences only.

### Files

- `docs/tier-review-model.md`, "Retiring a control" — the paragraph beginning
  "**A rule needs a second instance**"
- `docs/tier-review-model.md`, "When review ends" — the Retired-when line of
  the paragraph beginning "**The repair is read whole**"

### Public surface

None added. The sentence is the published evidence for a rule an adopter
follows, so what an adopter reads is the correctness of the evidence, not a
new instruction.

### Behaviour

- After the change no number in either sentence lacks a site a reader can open
  or a command a reader can run.
- **This ticket adds no rule, so it states no falsifier.** The rule it applies
  is EM-024's, which carries its own.
- The map and the model's index are not touched: no section is added, removed
  or renamed, and the question either row settles does not move.

## Acceptance criteria

1. AC1: the second-instance sentence no longer states "eight" beside the list
   that enumerates the same eight, or states it with the list named as its one
   site.
2. AC2: the "thirteen" in that sentence is either produced by a command the
   sentence names, with its baseline in the same sentence, or is gone.
3. AC3: the "thirteen" in "When review ends" is either produced by a command
   the sentence names, with its baseline in the same sentence, or is gone; and
   `grep -n "thirteen" docs/tier-review-model.md` returns no line stating a
   count of this repository's own tickets.
4. AC4: the rules those two paragraphs state — the second-instance bar, and
   the read-whole obligation — are unchanged, shown by the diff.

## Out of scope

- Every other number in this repository's documents. `README.md`'s two commit
  counts for one project are EM-015's and are not touched here.
- A sweep of the repository for counts without a site. That sweep was run at
  EM-024's round-1 review and its findings are EM-024-002's; this ticket is
  the two sentences named in Files and nothing else.
- `docs/quality-gates.md`, "A count that describes the tree has one site that
  goes red", itself. If that section is wrong, the finding belongs to EM-024.

## References

- `docs/quality-gates.md`, "A count that describes the tree has one site that
  goes red" — the rule this applies
- EM-024 — the ticket that landed it, and the instances in its Context
- EM-024-002 — the sibling that owns the counts of this repository's own
  structure found by the sweep, including the gate count's five sites
- EM-015 — the other count defect on this board, on figures no command in this
  repository can produce, which is why it is a different repair

## Notes

Raised under the contributor policy's §4 while working EM-024: found, not
fixed in place. The instance is worth having on the record for a second
reason — it is the first evidence that the new section catches something in
this repository, which is the population its falsifier will eventually be read
over.
