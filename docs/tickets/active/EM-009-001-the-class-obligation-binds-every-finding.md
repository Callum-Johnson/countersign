---
id: EM-009-001
title: The class obligation binds every repaired finding and was priced on must-fixes
status: in-progress
tier: critical
complexity: S
dependencies: []
claimed_by: claude-opus-5
claimed_at: 2026-09-07
---

# EM-009-001 — The class obligation binds every repaired finding

## Context

Raised by the independent review of EM-009 (round 1, finding 7), which
recorded it for the maintainer rather than repairing it.

The contributor policy's §6 states the obligation as "For each finding
repaired": the executor names the class, enumerates the siblings, and for
each sibling gives the test that pins it and the count of tests that go
red, or writes "repair of the instance" in those words. Nothing in the rule
distinguishes a must-fix from a note.

EM-009's own Costs section priced the rule on must-fixes: "On OMN-021's 46
must-fixes ... an assumed three siblings each would be about 138 suite
runs". The reviewer of EM-009 counted this repository's closed records at
the time and found 55 findings against 5 must-fixes. Across this
repository's wave at 34dc12c the Review sections record 23 rounds and 22
must-fixes, and the same tables record several times that many findings,
most of them notes and most of them repaired in the round.

So the obligation falls on roughly an order of magnitude more repairs than
the cost section counted, and the ticket that introduced it did not price
what it actually charges.

## Specification

This ticket carries a question the contributor policy's §3 reserves to the
maintainer. Two of the three available answers narrow a control, and the
party the control is on does not get to remove it — which is the
separation-of-duties rule, applied to the executor that would otherwise
choose the cheaper reading.

The answers available, with what each costs:

1. **Leave it.** Every repaired finding carries a class or the words
   "repair of the instance". Cost: the enumeration is paid on wording
   notes, where a class question rarely has siblings and the honest answer
   is almost always "repair of the instance" — which trains the executor to
   write the phrase without asking the question, and a declaration written
   by habit is the decorative claim EM-014's falsifier exists to catch.
2. **Narrow to must-fixes.** Notes carry nothing. Cost: a note repaired one
   branch too shallow is exactly the defect EM-009 was raised for, and
   round 2 of EM-009's own review found one — a definition added for a
   note, which pointed at a section that did not exist. Narrowing here
   would have exempted it.
3. **Narrow by round.** A note repaired in the same commit as the round's
   must-fixes is covered by the must-fix's class statement, and carries
   nothing of its own. Cost: it makes the obligation depend on how the
   executor packages commits, which the executor chooses.

What the executor needs in order to proceed: the maintainer's choice, or a
different one. The implementer then amends §6, and the amendment carries a
record per "Retiring a control", since narrowing a rule is an amendment
with record and not a wording fix.

## Acceptance criteria

1. AC1: `docs/ai-contributor-policy.md` §6 states which findings the class
   obligation binds.
2. AC2: If the rule is narrowed, a decision record carries the rule's text
   as it stood, the finding that matched, and the new text, per
   "Retiring a control".
3. AC3: The pull-request description states the finding-to-must-fix ratio
   measured on this repository's closed records, with its baseline commit.
4. AC4: Critical tier per ADR-0002: an independent agent reviews this
   against the artifacts and records findings in two columns.

## Out of scope

- Any change to the falsification gate for original work.
- Any change to what a class is, or to how one is found.

## References

- `docs/ai-contributor-policy.md` §6 — the obligation.
- EM-009, "What this refuses, and what it costs" — the pricing this ticket
  contests, and its recorded review finding 7.
- `docs/tier-review-model.md`, "Separation of duties" — why the executor
  may not choose here.

**BLOCKER (2026-09-06):** the executor cannot proceed. The Specification
above states a question that §3 reserves to the maintainer: which findings
the class obligation binds. Answers 2 and 3 narrow a control that sits on
the executor, and "Separation of duties" is explicit that the party subject
to a control does not get to remove it. An executor choosing here would be
choosing how much its own repairs must justify themselves.

To proceed the executor needs the maintainer's choice among the three
answers stated above, or a fourth. Answer 1 needs no document change and
would close this ticket by recording the decision; answers 2 and 3 are an
amendment with record under "Retiring a control".

**Discharged (2026-09-07).** The maintainer answered the reserved question
and chose answer 2: the class obligation narrows to must-fixes. A repaired
finding the reviewer did not record as blocking merge carries nothing —
neither a class and its siblings nor the words "repair of the instance".
The `BLOCKER:` text above stands as the record of why the ticket stopped
and is kept rather than deleted.

The reasoning the maintainer gave, recorded here because the repository is
the only record there is: under the obligation as it stands, every note
repaired in this repository’s closed tickets came back declared "repair of
the instance" with no siblings enumerated, which is the declaration written
by habit that "Retiring a control" calls decorative.

The risk the maintainer accepted is the one answer 2 states above, and it
is not hypothetical. Round 2 of EM-009’s own review found a repair made
for a note — R1.6, the exit for a class with no finite enumeration — which
named "the stopping rule" without saying where it is, a section name no
document carries. Under the narrowed obligation that repair would have
carried nothing.

## PR Description

### Ticket
EM-009-001 — The class obligation binds every repaired finding and was
priced on must-fixes

### Tier
critical — process surface under the operative test: a rule every executor
works under changes meaning, and ADR-0002 governs the review.

### Summary
The contributor policy's §6 bound the class obligation to "each finding
repaired", while EM-009, which introduced it, priced it on must-fixes. The
maintainer answered the question this ticket reserved on 2026-09-07 and
narrowed the rule: the obligation binds a repaired must-fix, and a note
repaired in the round or at close carries nothing. ADR-0004 records the
amendment with the old text, the finding that prompted it, and the new text.

### Acceptance criteria
- [x] AC1: `docs/ai-contributor-policy.md` §6 states which findings the
  class obligation binds — "A review must-fix is repaired at its class — a
  must-fix being a finding the reviewer records as blocking merge, as 'When
  review ends' in `docs/tier-review-model.md` defines it", and, four
  sentences later, "**A note carries nothing.**" The class, the siblings,
  the test and red count per sibling, the "repair of the instance" wording,
  the no-finite-enumeration case and the no-suite case are unchanged;
  3258933 is the commit.
- [x] AC2: `docs/adr/0004-the-class-obligation-binds-a-repaired-must-fix.md`
  carries the rule's text as it stood, EM-009's round-1 finding R1.7 quoted
  from that ticket's closed record, and the replacement text, each in its
  own block — and, because R1.7 did not match the rule's stated falsifier,
  the old and new falsifier text with the reason the finding was not
  foreseen, which is the fourth bullet of "Retiring a control". Status is
  `proposed`; the closing commit moves it to `accepted`, as ADR-0003 was.
- [x] AC3: over the 34 review rounds recorded in this repository's closed
  tickets at 60f39fb whose rows state both counts, the Review tables hold 40
  must-fixes against 180 findings — a rule priced on must-fixes charged on
  four and a half times as many repairs — read at that commit by:

      grep -rh "^| [0-9] | [0-9]* (of [0-9]" docs/tickets/done/*.md \
        | sed -E 's/^\| [0-9]+ \| ([0-9]+) \(of ([0-9]+).*/\1 \2/' \
        | awk '{m+=$1; f+=$2; n++} END {print n, m, f}'

  Three further rounds, in EM-019-001-001, state a must-fix count without a
  finding count and are outside those figures. Nothing on this branch
  touches `docs/tickets/done/`, so the figures stand unchanged at 3258933;
  the closing commit adds this ticket to that directory and changes what the
  command counts, which is why the population is named as the closed tickets
  at 60f39fb rather than left to move.
- [ ] AC4: not met — round 1 is pending. The branch is left checked out at
  3258933 for an independent reviewer working in a worktree of its own.

**What the wider population bought, measured.** Four closed tickets at
60f39fb record repairs in §6's form — EM-009, EM-016, EM-019-001 and
EM-019-001-001 — listed by `grep -rl "^- R[0-9].*— \(class:\|repair of the
instance\)" docs/tickets/done/*.md`, with their repair lines from `grep -rn
"^- R[0-9]" docs/tickets/done/*.md` and each finding's must-fix status read
from its ticket's own Review row. Ten lines declare "repair of the
instance", covering eighteen findings, of which twelve are findings the
round did not record as must-fixes; all twelve declare the words and
enumerate no siblings. Six lines name a class, covering seven findings, and
every one of the seven is a must-fix. No repair of a note has named a class
in this repository.

**Which side of the decision-record line this falls on.** The record side.
`docs/adr-process.md`, "When to write one", triggers on a workflow rule
changing, and the paragraph beneath it — "What 'a workflow rule changes'
reaches", as EM-019-001-001 rewrote it — names "a rule retired or amended
under 'Retiring a control'" explicitly, "because there the record is the
control: the retired text leaves the document, and the record is the only
place it and the finding that matched survive". That is this change exactly:
the text binding every repaired finding leaves §6, and ADR-0004 is the only
place it, R1.7 and the old falsifier survive. The second side of the line
reaches a rule added inside a document or extended in place under an
existing decision, whose ticket is its own record; this is neither an
addition nor an extension but a narrowing of reach, and the ticket file
cannot be the record because the text that left it is not in the ticket. The
section's one-question test — does the decision affect multiple tickets or
constrain future work — answers the same way, so EM-019-001-001-001, open in
`ready/` on the test reading wider than the line, does not change the answer
here.

**Who worked this, and why that is allowed.** "Retiring a control" says a
retirement or amendment ticket is not worked by the executor whose work the
rule refused. The finding was recorded by EM-009's independent reviewer
against the rule EM-009 was adding, and EM-009 was executed by
`claude-fable-5-1`, which also held this ticket when it blocked; the
executor here is `claude-opus-5`, a different party. The rule's cost falls
on every executor closing a ticket, this one included, which is why the
narrowing was not the executor's to choose at all: two of the three answers
narrow a control that sits on the executor, "Separation of duties" reserves
that, the ticket blocked under §3 on 2026-09-06, and the maintainer answered
on 2026-09-07. The `BLOCKER:` text is kept above and marked discharged.

**The second-instance bar does not reach this.** "A rule needs a second
instance" states that the bar "does not reach a repair of the change under
review, an entry in a list, or an amendment under this section". This is an
amendment under that section, and it adds no rule.

### Falsification
N/A — a documentation change with no behavioural claim and no suite. What a
reader does differently, per criterion:
- AC1: an executor repairing a review round now asks of each finding whether
  the reviewer recorded it as blocking merge. For a must-fix nothing
  changes — the class, the siblings, and a red count or "repair of the
  instance", as before. For a note it writes no Falsification line at all:
  it repairs the note, and the description records it only where the Review
  findings list already records the finding. Concretely, on the four
  tickets counted above at 60f39fb the executor would have owed twelve
  fewer declarations and lost no class, since none of the twelve named
  one.
- AC2: a later contributor who finds §6 narrower than EM-009 left it reads
  ADR-0004 and sees a decision with its evidence, rather than inferring that
  a rule was quietly relaxed and restoring it.
- AC3: a maintainer deciding whether to widen the rule again has the
  population it was narrowed on, and the falsifier's second arm names the
  evidence that would ask for the widening.
- AC4: nothing; it is the guard.

No review finding has been repaired on this branch, so §6's own repair form
records nothing here. Round 1 is pending.

### Out of scope (per ticket)
Confirmed: the falsification gate for original work is untouched, and
nothing changes what a class is or how one is found — the amendment moves
which findings the obligation reaches and nothing else.

Beyond the ticket's References and declared here: the repair paragraph of
`templates/PR-DESCRIPTION.md`, which states the same trigger in the form a
description is written from. Two descriptions of one rule that disagree is
the drift EM-007-001 was raised for, and amending §6 while leaving the
template saying "for each review finding repaired" would have been the
repair one branch too shallow this ticket exists to prevent.

Declared: the §6 bullet was re-wrapped whole rather than patched line by
line. No word outside the amendment changed. Patching in place would have
left short lines mid-paragraph, which this repository's reviews have twice
recorded as findings — EM-009 round 2, "two ragged lines from round-1
repairs", and EM-019-001 round 2, "a ragged paragraph".

The map in `docs/ai-contributor-policy.md`, "Which document settles what",
and the index in `docs/tier-review-model.md`, "What is in this document",
needed no change: no governed document was added, removed or renamed; no
section was added, removed or renamed; and where the question "what must be
true before I report this change done?" is settled did not move — it is §6
before and after. `docs/adr/0004-...` is a decision record, which that rule
names as a document it does not govern, and the map's row for `docs/adr/` is
a directory row, which the rule keeps true as a row and not one row per file
beneath it.

Recorded, not changed: `docs/quality-gates.md`, "A test pins a claim, not a
mechanism", says the gate's companion "for the repair of a review finding"
is stated in §6 and not restated there. It points rather than states, and §6
is where the trigger is settled, so it is left as it stands and named here
so a reader who notices finds it decided rather than missed.

### How to verify
1. `git show 3258933` — the amendment to §6, the matching paragraph of
   `templates/PR-DESCRIPTION.md`, and ADR-0004, in one commit.
2. `sed -n '/^## 6\./,/^## 7\./p' docs/ai-contributor-policy.md` — §6
   whole, as "When review ends" asks it be read before it is handed back.
3. `git show 60f39fb:docs/ai-contributor-policy.md | sed -n '246,266p'` —
   the rule and its falsifier as they stood at the branch point, to check
   against the two "as it stood" blocks quoted in ADR-0004.
4. `grep -n -A 6 "R1\.7" docs/tickets/done/EM-009-a-review-*.md` — the
   finding the record quotes, in the ticket that recorded it.
5. Re-run the counting commands above; the population they read,
   `docs/tickets/done/`, is untouched by this branch.

### Risks / follow-ups
The risk the maintainer accepted, restated so it is not lost: a note
repaired one branch too shallow is now exempt, and that is the defect EM-009
was raised for. Round 2 of EM-009's own review found one — round 1's repair
of R1.6, a note, named "the stopping rule" without saying where it is, a
section name no document carries. Under this amendment that repair would
have carried nothing. The falsifier's second arm is where the evidence goes
if it recurs: a repair made for a finding the reviewer did not record as a
must-fix drawing a finding inside that repair in a later round, more than
once over a stated population of closed tickets, read from the Review tables
that already carry each round's findings, which of them blocked merge, and
how many sat inside the previous round's fix.

The class signal in `docs/tier-review-model.md`, "What a review reports",
asks for §6's form on a trigger of its own and does not require either
finding to be a must-fix. §6 now says the exemption is from that bullet
only, so the two rules do not disagree. Narrowing the class signal as well
is reserved the same way this question was, and would be its own ticket.

ADR-0004 is `proposed`. The commit that closes this ticket moves it to
`accepted`, which is the practice ADR-0003 established.

No child ticket was raised: nothing outside the amendment was found needing
work.

### Review
| Round | Must-fix | Where (rules / lists / documents / tests) | Inside previous round's fix | Repaired by |
|---|---|---|---|---|
| 1 | — | — | — | — |

Round 1 pending. The total is derived from the rows and is not asserted
beside them.
