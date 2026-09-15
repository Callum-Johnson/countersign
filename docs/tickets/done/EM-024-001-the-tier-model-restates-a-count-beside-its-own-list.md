---
id: EM-024-001
title: The tier model restates a count beside its own list
status: done
tier: standard
complexity: S
dependencies: [EM-024]
claimed_by: claude-opus-5
claimed_at: 2026-09-15
closed_at: 2026-09-15
---

# EM-024-001 — The tier model restates a count beside its own list

## Context

EM-024 lands `docs/quality-gates.md`, "A number determined elsewhere has one
site that goes red", which asks that a number something other than its own
sentence determines have one site, that the site be one that fails when what it
counts moves, and that every other mention name the site rather than the
number. The first thing that section binds is this repository, and
`docs/tier-review-model.md` carries non-complying sentences in two of its
sections, both of them stating "thirteen", and one of them restating "eight"
twice over.

**The first**, in "Retiring a control", in the paragraph beginning "**A rule
needs a second instance**", reads: "Of the thirteen rule-adding tickets from
EM-006 to EM-020, eight name one source ticket on one project in their
Context — EM-007, EM-008, EM-010, EM-011, EM-012, EM-012-001, EM-014-001 and
EM-019-001 — counted by reading each Context for the source it names." Two
counts, two defects, one sentence:

- **"eight" is restated beside its own list.** The enumeration that follows it
  is its determiner and its site. The number is a second copy of what the list
  already says, and the two can disagree the moment a ticket is added to or
  removed from the list — which is exactly the shape EM-024's Context records
  four times over. **And it is restated again three lines later**, at
  `docs/tier-review-model.md:493`, "Those eight are this rule's instances" —
  a third copy of one list, in one paragraph. That site was left unraised by
  EM-024's round-1 sweep and was found by its round-2 independent review; it is
  folded in here rather than raised separately, for the same reason the second
  "thirteen" was, and because a repair that corrected one of a paragraph's two
  copies and left the other standing would be the duplication failure the
  section is about, committed inside the repair of that failure.
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

Both sentences keep their evidence and lose their unpinned numbers. The changes
below are independently decidable by the executor:

- The enumeration stays and every restatement of "eight" goes, or "eight"
  stays at one place and the enumeration moves to a site that place points at.
  The first is the cheaper reading and is what OMN-024's round 3 chose for its
  own sibling list; the ticket does not mandate it. Whichever is chosen reaches
  both copies — the one in the sentence that carries the list, and "Those
  eight" in the sentence after it. Repairing one is the failure this ticket
  documents.
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
  "**A rule needs a second instance**", both of its restatements of "eight" and
  its "thirteen"
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

1. AC1: neither the second-instance sentence nor the sentence after it states a
   count beside the list that enumerates it; the list is the one site, or the
   number is stated once with the list named as that site.
   `grep -n "eight" docs/tier-review-model.md` returns no line restating a count
   of that list.
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
- A sweep of the repository for numbers whose determiner is not named. That
  sweep was run at EM-024's round-1 review, rebuilt at its round 3, and its
  findings are EM-024-002's; this ticket is the sentences named in Files and
  nothing else.
- `docs/quality-gates.md`, "A number determined elsewhere has one site that
  goes red", itself. If that section is wrong, the finding belongs to EM-024.

## References

- `docs/quality-gates.md`, "A number determined elsewhere has one site that
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
this repository, and a finding recorded under that section is the unit its
falsifier is read over.

**Widened at EM-024's round-2 review**, under §4 and again found rather than
fixed: `docs/tier-review-model.md:493` restates "eight" a second time, in the
paragraph this ticket already owns. Folded in here so that one paragraph's
copies are repaired together.

## PR Description

### Ticket
EM-024-001 — The tier model restates a count beside its own list.

### Tier
`standard`, on one independent review pass. A change to
`docs/tier-review-model.md` is a change to a process document, which "The
operative test" fixes at that tier. The pass ran against 77374a1 and is row 1
of the Review table.

**On the dependency.** The frontmatter names EM-024, which is `in-progress`
rather than `done`. The rule this ticket applies —
`docs/quality-gates.md`, "A number determined elsewhere has one site that goes
red" — landed on the default branch at d669ead on 2026-09-09, under the
maintainer's direction to split EM-024: land the rule, leave the ticket open
for its record defects and its siblings. What EM-024 still holds open is its
own record, not the rule. The dependency is on the rule and the rule is in
force, which is why this was worked rather than held; EM-024's Notes record
the maintainer's acceptance that a ticket and its diff parting ways is
undescribed by `docs/ticket-lifecycle.md`.

### Summary
Two evidence sentences in `docs/tier-review-model.md` kept a number beside the
thing that determines it. The second-instance paragraph stated a count of
rule-adding tickets and then stated the size of its own enumeration twice; the
read-whole Retired-when stated a count over a denominator. All four numbers
are gone, the lists and ranges that determine them remain, and the Retired-when
names the site that carries the pre-rule rate rather than restating it.

### Acceptance criteria
- [x] AC1: neither the second-instance sentence nor the sentence after it
  states a count beside the list that enumerates it. `grep -n "eight"
  docs/tier-review-model.md`, run after b57e220, returns one line — 402, "the
  eight rules it built were unchanged after round 6". That is a count of
  OMN-021's rules on the control-plane project, whose determiner is not in
  this tree; it is not a restatement of this list, and the ticket's Out of
  scope holds every other number regardless. Both restatements are gone: the
  list-bearing sentence and "Those are this rule's instances" carry no count.
- [x] AC2: the "thirteen" in that sentence is gone, which is the criterion's
  second option. The range "from EM-006 to EM-020" and the enumeration remain,
  and the sentence now names how both the population and the predicate were
  found, so a reader can rebuild the same set.
- [x] AC3: the "thirteen" in "When review ends" is gone. `grep -n "thirteen"
  docs/tier-review-model.md`, run after b57e220, returns nothing.
- [x] AC4: the rules those two paragraphs state are unchanged. The second-
  instance bar — "A failure met once is recorded where it was met … is not
  written into these documents as a rule until it is met a second time" — its
  carve-outs, the sentence binding the bar to tickets raised after the ticket
  that landed the paragraph, the read-whole obligation and the Retired-when's
  trigger clause are all byte-identical. Every changed line is evidence. Rule
  sentences appear inside the hunks only because the evidence re-flowed around
  them, which the same section says is not a finding.

### Falsification
N/A for a behavioural claim — this repository publishes documents and runs no
suite. Per criterion, what a reader does differently: a reader checking either
sentence opens the list or the paragraph that determines the figure, instead
of reading a number that nothing in the tree would contradict if it drifted.

For the review finding repaired, per the contributor policy's §6:

- R1.1 — class: **which numbers did this change leave in the two paragraphs it
  edited, and does each have one site?** The surviving "five" in the
  Retired-when is the instance. The question was asked of every number left in
  both paragraphs after 77374a1. Siblings, each checked:
  - **"five", in the read-whole Retired-when** — the instance. The paragraph's
    opening sentence already carries the same claim with its baseline *and* its
    determiner: "On this repository's closed records at 5d94db7, every must-fix
    found after a first round sat inside the previous round's own repair — five
    of five, per the Review tables of the closed tickets". The first repair
    left a second copy carrying the baseline and not the determiner, so the
    section had two sites for one number and the weaker one was the copy.
    Repaired: the Retired-when names the paragraph above as the site and
    restates nothing.
  - **"5d94db7", both occurrences** — checked and sound. A commit hash names
    something rather than measuring it; §6's own test is whether a command
    could disagree with the number, and no command disagrees with an
    identifier.
  - **"EM-006 to EM-020", and the eight ids in the list** — checked and sound
    for the same reason: ticket ids name rather than measure.
  - **"more than once"** in the Retired-when trigger — checked and sound. It is
    the rule's threshold, not a measurement of the tree, and nothing else
    determines it.
  What a reader does differently: a reader who wants the pre-rule rate reads
  the one sentence that carries it with the records it was read from, rather
  than two sentences fourteen lines apart that could drift against each other.
- R1.3 — note. Repaired in the round; a note carries nothing under §6 as
  EM-009-001 narrowed it. The sentence now names how the population was
  enumerated as well as how the predicate was tested.
- R1.2 — note, and it falls away with R1.1's repair. It asked that a number
  kept under the section's exception record which determiner it copies and why
  naming it would not serve the reader. No number is kept in that sentence, so
  no declaration is owed.

### Out of scope (per ticket)
Confirmed; nothing here exceeds it.
- Every other number in this repository's documents — untouched. `README.md`'s
  two commit counts are EM-015's and are not touched.
- A sweep of the repository for numbers whose determiner is not named —
  not run. That is EM-024-002's.
- `docs/quality-gates.md` itself — untouched. `git diff main...HEAD
  --name-only` names `docs/tier-review-model.md`, this ticket file and the
  board.

### How to verify
1. `grep -n "eight\|thirteen" docs/tier-review-model.md` — one hit, line 402,
   which is OMN-021's rules and outside this ticket.
2. `sed -n '/^\*\*The repair is read whole/,/protects nothing\./p' docs/tier-review-model.md`
   — the paragraph and its Retired-when; the rate appears once, in the opening
   sentence, with its baseline and the records it came from.
3. `sed -n '/^\*\*A rule needs a second instance/,/is not ready\./p' docs/tier-review-model.md`
   — the second-instance paragraph; the list appears once and no sentence
   states its size.
4. `git diff main...HEAD -- docs/tier-review-model.md` — two hunks, both
   confined to evidence sentences, which is AC4.

### Risks / follow-ups
- **The list is an exhaustive claim with nothing that goes red.** "Those
  naming one source ticket on one project in their Context are EM-007, …" is a
  complete claim over a range, and sub-tickets fall inside that range —
  EM-012-001 and EM-019-001 are in the list — so a future EM-0xx-001 that
  names one instance silently falsifies it. The sentence now says how both the
  population and the predicate were found, which is the most this repository
  can do without a suite, and the reviewer confirmed the claim was exhaustive
  before this change too, so no new instance of that failure mode is
  introduced. `EM-026`, open in `ready/`, owns the general case.
- Line 446 of the document runs long against the file's usual measure. It ran
  long before this change for the same reason, and "The repair is read whole"
  says a repair does not re-flow text it did not change, so it is left.

### Review
One independent review pass, per "The operative test" for a change to a
process document. No second pass is taken.

| Round | Must-fix | Where (rules / lists / documents / tests) | Inside previous round's fix | Repaired by |
|---|---|---|---|---|
| 1 | 1 (of 3 findings) | documents: the read-whole Retired-when still stated "five" while the paragraph's opening sentence already carried the same claim with its baseline and its determiner, so the section had two sites for one number and the copy left was the one without the determiner (must-fix); the commit message recorded the baseline but not which determiner the number copied, which the section's own exception requires of a number kept; the rewritten second-instance sentence names a method for its predicate and not for its population, so an exhaustive claim is checkable only by rebuilding the set | — | b57e220 |

Derived from the row and not asserted beside it: one must-fix over one review
round. Round 1 has no round before it, so its inside-previous-fix cell reads
`—` and no line is uncountable.

- R1.1 · permits · must-fix · `docs/quality-gates.md`, "One site, and every other mention names the site rather than the number", and the ticket's Behaviour, "After the change no number in either sentence lacks a site a reader can open or a command a reader can run" · the change removed one unpinned number and left another; the surviving "five" restates the paragraph's opening sentence, which already carries the baseline and the determiner, so two sites hold one number and the weaker is the copy — remedy: make the Retired-when name the site instead of restating it, or drop the sentence; cost, if the remedy tightens a control: none, it deletes a copy and adds no obligation; inside previous fix: —
- R1.2 · permits · note · `docs/quality-gates.md`, "Where a number is written anyway, the exception is not the writer's to take silently" · the commit message recorded the baseline but not which determiner the five copies, nor why naming it would not serve the reader — remedy: take R1.1's remedy, after which no declaration is owed; cost: none; inside previous fix: —
- R1.3 · permits · note · `docs/quality-gates.md`, "an enumeration claimed complete and actually short is worse than one declared open with its coverage stated" · the rewritten sentence names how the predicate was tested but not how the population was enumerated, so an exhaustive claim over a range is checkable only by rebuilding the set — remedy: name both; cost: none; inside previous fix: —

The reviewer found nothing in the second column and recorded that as an
answer. It tested two candidates and rejected both: dropping the denominator
does not break the falsifier, because the trigger reads on an absolute
threshold over a population a future reviewer states and the pre-rule rate
survives in the paragraph above; and the recast past tense keeps the baseline
evidence distinct from the post-rule population the falsifier measures, which
is what stops the rule reading as born-retired.

### Definition of Done (all tiers)
The four machine checks do not apply to a repository that publishes documents
and runs no suite; the falsification gate is discharged above, with N/A for
the behavioural claim and a class line for the must-fix repaired. Every
measured figure names its baseline in the same sentence and is read from the
command named beside it. The independent pass a process-document change takes
has run and is recorded.
