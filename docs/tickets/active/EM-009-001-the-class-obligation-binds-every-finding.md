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
Round 1 of the independent review found that the narrowing turned on a fact
the record did not carry, and the repair is at that class: every finding line
now carries the rank the reviewer gave the finding and, where it sits inside
the previous round's fix, the finding whose repair it sits inside.

### Acceptance criteria
- [x] AC1: `docs/ai-contributor-policy.md` §6 states which findings the
  class obligation binds — "A review must-fix is repaired at its class — a
  must-fix being a finding the reviewer records as blocking merge, as 'When
  review ends' in `docs/tier-review-model.md` defines it", and, four
  sentences later, "**A note carries nothing.**" The class, the siblings,
  the test and red count per sibling, the "repair of the instance" wording,
  the no-finite-enumeration case and the no-suite case are unchanged.
  Since round 1, §6 also states that the rank is the reviewer's and carried
  finding by finding, that the executor transcribes it and does not re-rank,
  and that a finding the reviewer left unranked is repaired at its class as a
  must-fix is; and the carried-forward sentence on a class with no finite
  enumeration, ungrammatical since EM-009, now reads "is recorded the way the
  third condition ... records a list". Since round 2 it also bars renumbering
  and merging the reviewer's findings alongside re-ranking them, because the
  finding number is what the falsifier's second arm and the
  inside-the-previous-fix field read, and says that naming several findings in
  one repair line is not a merge. 3258933 is the amendment, 8e87a58 the
  round-1 repair and f8880b5 the round-2 repair.
- [x] AC2: `docs/adr/0004-the-class-obligation-binds-a-repaired-must-fix.md`
  carries the rule's text as it stood, EM-009's round-1 finding R1.7 quoted
  from that ticket's closed record, and the replacement text, each in its
  own block — and, because R1.7 did not match the rule's stated falsifier,
  the old and new falsifier text with the reason the finding was not
  foreseen, which is the fourth bullet of "Retiring a control". Since round 1
  it also records the record's new fields, names the authority for each half
  of the amendment — that fourth bullet for widening the falsifier, the
  maintainer's §3 answer for narrowing the rule, and not the third bullet,
  whose precondition is a match that did not occur — and gives the second arm
  a standing count. Since round 2 it also states the template change as a
  consequence of the narrowing, on the maintainer's condition of 2026-09-07:
  what changed, why the narrowing required it, and what it costs each review
  record. Status is `proposed`; the closing commit moves it to `accepted`, as
  ADR-0003 was.
- [x] AC3: over the 34 review rounds recorded in this repository's closed
  tickets at 60f39fb whose rows state both counts, the Review tables hold 40
  must-fixes against 180 findings — a rule priced on must-fixes charged on
  four and a half times as many repairs — read at that commit by:

      grep -rh "^| [0-9] | [0-9]* (of [0-9]" docs/tickets/done/*.md \
        | sed -E 's/^\| [0-9]+ \| ([0-9]+) \(of ([0-9]+).*/\1 \2/' \
        | awk '{m+=$1; f+=$2; n++} END {print n, m, f}'

  Three further rounds, in EM-019-001-001, state a must-fix count without a
  finding count and are outside those figures. Nothing on this branch
  touches `docs/tickets/done/`, so the figures stand unchanged; the command
  was re-run at 8e87a58, after the round-1 repair, and at f8880b5, after the
  round-2 repair, and returned the same 34 40 180 both times. With `f/n`
  printed as well it returns a mean of 5.29 findings per round at 60f39fb,
  which is what a rank on every finding line costs a review record and is
  recorded with the template change in ADR-0004. The closing commit adds this ticket to that directory and
  changes what the command counts, which is why the population is named as
  the closed tickets at 60f39fb rather than left to move.
- [ ] AC4: rounds 1 and 2 are complete and round 3 is pending. The
  independent review of a586c67 returned 3 must-fixes over 8 findings,
  repaired at 8e87a58; the review of 24d81a8 returned 2 must-fixes over 5
  findings, both inside round 1's fix, repaired at f8880b5. The class signal
  in "What a review reports" fired on R2.2, and the repair is a redesign
  against its class rather than the adjustment the reviewer recorded beside
  the signal. Both rounds are in Review below. The branch is left checked out
  for the next round, which is the third and last before the cap.

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
  instance", as before. For a note it need write no Falsification line: it
  repairs the note, and the description records it in the Review findings
  list, which carries every finding. To tell whether a line is owed it reads
  the rules that ask for the class form, not a list of exceptions in the
  template: §6 asks the form of a repaired must-fix and of the repair of a
  finding the reviewer left unranked, and the class signal in "What a review
  reports" asks it of the round's repair of the rule the signal fired on,
  whatever the two findings' ranks. Concretely, on the four tickets counted above at 60f39fb the executor
  would have owed twelve fewer declarations and lost no class, since none of
  the twelve named one. It also reads the rank off the finding line rather
  than parsing "(must-fix)" out of a prose cell, and does not set it.
- AC2: a later contributor who finds §6 narrower than EM-009 left it reads
  ADR-0004 and sees a decision with its evidence, rather than inferring that
  a rule was quietly relaxed and restoring it.
- AC3: a maintainer deciding whether to widen the rule again has the
  population it was narrowed on, and the falsifier's second arm names the
  evidence that would ask for the widening.
- AC4: nothing; it is the guard.

**Round 1's must-fixes, in §6's form.** Two classes, not one. The
record-fields question stated first produces R1.1, R1.2 and R1.4 and does not
produce R1.3, whose subject is a landing of the rule that failed to carry
one of §6's exceptions rather than a fact the record must hold; a single
class covering all three would have been named to fit the findings instead
of generating them, which is the declaration by habit the obligation exists
to prevent. There is no suite, so each sibling says what a reader does
differently.

- R1.1 — class: **on what fields of the record does the narrowed rule, its
  falsifier, the template and ADR-0004 depend, and does the record carry
  them?** Siblings the question enumerates, each checked against the record
  at 60f39fb:
  - §6's trigger, "a repaired must-fix" — needs the rank of each finding.
    The record carried a per-round must-fix count and "(must-fix)" in the
    prose of the Where cell, tied to no numbered finding. Missing; the rank
    is now on every finding line, and a reader deciding whether a repair owed
    a class reads that line instead of parsing a prose cell.
  - §6's exemption, "A finding the reviewer did not record as a must-fix" —
    the same field, read the other way, and the same gap. A reader now sees
    which findings the exemption covered rather than inferring it.
  - Who sets the rank — the executor writes the description and transcribes
    the review, so nothing stopped it re-ranking. §6 now says the rank is the
    reviewer's and the executor does not re-rank, as it already routes a
    finding under the second condition of "When review ends" without
    reclassifying it. A reviewer checking a repair now has a claim to check.
  - Silence, which is R1.4 — nothing obliges a reviewer to rank, and an
    unranked finding defaulting to exempt would hand the scope back to the
    executor. §6 now repairs an unranked finding at its class as a must-fix
    is. A reader sees that no gain follows from a rank being missing; raising
    one's own obligation is self-imposed cost under "Separation of duties"
    and needs no second party.
  - The falsifier's second arm, which is R1.2 — needs the rank of the earlier
    finding and the identity of the fix a later finding sits inside. The
    record carried an aggregate `m of n` and a yes/no. Both now on the line:
    the inside-the-previous-fix field names the finding whose repair the
    finding sits inside. A reader can now count the arm.
  - The arm's population, also R1.2 — a note repaired before this rule
    carried the obligation, so it is no evidence about the exemption, and the
    arm as written took the whole record as its population. It now counts
    only rounds recorded under this rule. A reader knows which rounds count.
  - The arm's standing count, which is R1.5 — the record carried no count, so
    no reader could see how close the arm sat to firing. ADR-0004 now states
    it. A reader sees zero, over zero such rounds, and beside it the eleven
    times over the 34 rounds at 60f39fb that a finding in a later round sat
    inside the repair of a finding its round did not record as blocking
    merge. No command produces that eleven: it was obtained by reading every
    round after the first in `docs/tickets/done/` at 60f39fb for the prose
    naming the earlier finding or remedy a later finding sits inside, and
    reading that finding's rank from its own round's Where cell — seven named
    outright by the record, four matched from the remedy that introduced the
    text, and three rounds unattributable because they name no earlier
    finding at all. ADR-0004 carries the list and the method; that reading is
    the labour the two new fields remove.
  - The first arm, "repairs declared 'repair of the instance' draw a sibling
    finding in the next round" — needs which repair a later finding is a
    sibling of. The inside-the-previous-fix field now names it, so the arm
    that predates this ticket is readable too. Checked and left otherwise as
    it stands: its wording is EM-009's and outside this ticket.
  - The class signal in "What a review reports" — needs the column and
    whether the finding sits inside the previous fix. Both still carried, and
    naming the finding rather than answering yes still answers whether. A
    reader of that signal does nothing differently, which is the point: the
    maintainer did not narrow it.
- R1.2 — sibling of R1.1's class, above; it falls out with the question, and
  its own remedy — state the arm on the fields the record has, or add the
  linking field — is the second of those, taken.
- R1.3 — class: **which of §6's qualifications does each other statement of
  the obligation carry?** Siblings:
  - `templates/PR-DESCRIPTION.md`, the repair paragraph — carried the trigger
    and not the saving clause, so it forbade the line the class signal
    demands. Repaired: "need carry no line here, except where the class
    signal ... has fired". A reader who asked the class question on a note
    and found siblings may now record them, and must where the signal fired.
  - The same sentence's force, which is R1.6 — "carries no line" prohibits
    where §6 says "owes", and ADR-0004's own Neutral consequence says
    recording more costs a later reader nothing. Repaired by the same words.
  - `templates/PR-DESCRIPTION.md`, the Review finding-line prose — states the
    form, not the obligation, and now names the rank and the linking field
    and says whose they are. A reader transcribing a round knows what to
    write and what not to decide.
  - ADR-0004's Decision — carries the exemption and the saving clause
    already, and now the record's form. Checked, no gap.
  - `docs/quality-gates.md`, "A test pins a claim, not a mechanism", and
    `docs/tier-review-model.md`, "Repairs of repairs" and the class signal —
    all three point at §6 and state no qualification of their own, so there
    is nothing to carry. Checked, no gap; this is why the map's rows did not
    move.

**The falsifier is now readable from the record.** What would make the second
arm fire: two or more findings, in rounds recorded under this rule, whose
`inside previous fix` field names a finding whose own line is ranked `note`.
Where a reader would look: the finding lines under each round's row in the
Review section of every closed critical-tier ticket — three fields on one
line, the rank, the column and the fix it sits inside. Before this repair the
arm named the rank of a finding and the identity of a fix, and the record
carried neither, which is why round 1 called it decorative as written.

No behavioural claim is added by any of this; the lines above are what §6's
form asks of a repair, and the notes R1.4 to R1.8 carry no line of their own
except where they fall out of a class above.

**Round 2's must-fixes, in §6's form.** Two must-fixes, two classes. The
class signal in "What a review reports" fired on R2.2 and asks the same form
of the round's repair of that rule; both lines are owed here in any case,
since the reviewer ranked both findings must-fix. There is no suite, so each
sibling says what a reader does differently.

- R2.1 — class: **does the record's sole statement of its own form model any
  field of a finding line as settled by another, where the tier review model
  says the two are independent?** Siblings, each checked against
  `templates/PR-DESCRIPTION.md` at 24d81a8:
  - The rank on the two exemplars — written as the literals `must-fix` on the
    `permits` line and `note` on the `refuses` line, the only field fixed
    where every other is a placeholder, so the sole worked example of a
    finding line taught that rank follows column. That is what "What a review
    reports" forbids and what its own falsifier watches for. Repaired:
    `<rank>` on both lines, and the prose above them names the two values and
    says the column does not settle them. A reviewer's second-column must-fix
    — which R2.2 is — now has an exemplar that admits it.
  - The inside-the-previous-fix field on the second exemplar — the literal
    `no` where the first carried the placeholder, so the exemplar modelled a
    note as never sitting inside a fix, which is the pair the falsifier's
    second arm counts. Repaired: the full placeholder on both lines.
  - The cost clause, carried by the `permits` exemplar only — checked, no
    gap: it is written as a condition, "cost, if the remedy tightens a
    control", and "What a review reports" ties the cost to a remedy that adds
    to a control rather than to a column, so the exemplar states a condition
    and not a determination.
  - The column words themselves, `permits` and `refuses` — checked, no gap:
    the two lines exist to show the two columns, which are a closed pair the
    model names, and not a field with a value to fill in.
  - The round table's exemplar rows — checked, no gap: round 1's
    inside-the-previous-fix cell is `—` because no round precedes it, which
    the sentence under the table states, and round 2's is `<m of n>`.
- R2.2 — class: **which statements of the record's form carry an obligation
  as an exception to a prohibition, so that every rule wanting the form
  arrives as another exception with a scope written by hand?** Siblings:
  - The template's owed-line paragraph — the instance, repaired by the
    redesign recorded in the Review section below.
  - §6's saving clause, "That exemption is from this bullet only; the class
    signal ... asks for the same form on a trigger of its own, which this
    narrowing does not reach" — checked, no gap: it disclaims reach and
    points at the other rule instead of restating that rule's trigger, so it
    cannot drift from it and needs no scope of its own.
  - ADR-0004's Decision, "The exemption is from that bullet only" — checked,
    no gap, for the same reason.
  - Any other statement under `docs/` or `templates/` that carries an
    obligation as an exception — checked, none. `git grep -n "except
    where\|except that\|, except" 24d81a8 -- docs/'*.md' templates/'*.md'`,
    with the ticket directory excluded, returns the repaired sentence and
    nothing else; the same grep on the tree after the repair returns nothing.
    The one other exemption in the documents, "Who this binds" in
    `docs/tier-review-model.md`, exempts a closed population named in a
    decision record: it cannot grow, so it needs no scoping and is not a
    sibling.

The notes R2.3, R2.4 and R2.5 carry no line of their own; §6 does not reach
them and no other rule asks.

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

Declared: the §6 bullet was re-wrapped whole at 3258933 rather than patched
line by line. No word outside the amendment changed. Patching in place would have
left short lines mid-paragraph, which this repository's reviews have twice
recorded as findings — EM-009 round 2, "two ragged lines from round-1
repairs", and EM-019-001 round 2, "a ragged paragraph".

Beyond the ticket's References and declared, round 1: the Review finding-line
form in the same template. The narrowed rule and its falsifier depend on two
facts the record did not carry, and a rule whose evidence cannot be read is
the defect "Retiring a control" exists to remove; leaving the form alone
would have shipped a decorative falsifier. The form is stated in that
template alone — `grep -rln "inside previous fix" --include=*.md . | grep -v
"docs/tickets/"` returns `templates/PR-DESCRIPTION.md` and nothing else at
8e87a58 — so no second description of it drifts. The second-instance bar does
not reach the addition either: it "does not reach a repair of the change
under review", and this is one.

Declared, round 1: only what the round-1 remedies moved was re-wrapped. In
§6, everything above the sentence beginning "A class with no finite
enumeration" is byte identical to 3258933, and the tail below it re-wraps
because the inserted sentences moved the wrap; in ADR-0004 the two "as it
stood" blocks are untouched and the two replacement blocks are re-taken from
§6 as it now reads. The whole-bullet re-wrap at 3258933 is what let an
ungrammatical carried-forward sentence into that replacement-text block,
which is round 1's R1.8, and it is repaired in both places.

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
   `templates/PR-DESCRIPTION.md`, and ADR-0004, in one commit; `git show
   8e87a58` — the round-1 repair across the same three files.
2. `sed -n '/^## 6\./,/^## 7\./p' docs/ai-contributor-policy.md` — §6
   whole, as "When review ends" asks it be read before it is handed back.
3. `git show 60f39fb:docs/ai-contributor-policy.md | sed -n '246,266p'` —
   the rule and its falsifier as they stood at the branch point, to check
   against the two "as it stood" blocks quoted in ADR-0004.
4. `grep -n -A 6 "R1\.7" docs/tickets/done/EM-009-a-review-*.md` — the
   finding the record quotes, in the ticket that recorded it.
5. Re-run the counting commands above; the population they read,
   `docs/tickets/done/`, is untouched by this branch.
6. `sed -n '/^Findings, per round/,/^```/p' templates/PR-DESCRIPTION.md` —
   the finding line as it now stands, with the rank and the finding whose
   repair a finding sits inside, the sentence saying whose those two fields
   are, and two exemplars neither of which fixes a rank.
7. `sed -n '/^For each repair a line here/,/costs a later reader nothing.$/p'
   templates/PR-DESCRIPTION.md` — which repairs owe a class line, stated by
   naming the rules that ask for the form. Ask of any finding whether a line
   is owed, and check that answering needed no clause about a previous
   amendment.
8. Read the Review section below and ask, of any closed round, what would
   retire the exemption: two findings whose `inside previous fix` names a
   finding ranked `note`. Round 1 below has none — every finding sits
   inside nothing, since it is the first round — which is what a readable
   falsifier looks like when it has not fired.

### Risks / follow-ups
The risk the maintainer accepted, restated so it is not lost: a note
repaired one branch too shallow is now exempt, and that is the defect EM-009
was raised for. Round 2 of EM-009's own review found one — round 1's repair
of R1.6, a note, named "the stopping rule" without saying where it is, a
section name no document carries. Under this amendment that repair would
have carried nothing. The falsifier's second arm is where the evidence goes
if it recurs: a finding in a later round sitting inside the repair of a
finding the reviewer ranked a note, more than once over a stated population
of closed tickets. Round 1 found that the record could not produce that
evidence, and the arm now reads from the two fields this ticket added to the
finding line — the rank, and the finding whose repair a finding sits inside.
It counts only rounds recorded under this rule, since a note repaired while
the obligation still bound it says nothing about the exemption; its standing
count and the eleven historical near-instances over the 34 rounds at 60f39fb
are in ADR-0004.

The class signal in `docs/tier-review-model.md`, "What a review reports",
asks for §6's form on a trigger of its own and does not require either
finding to be a must-fix. §6 now says the exemption is from that bullet
only, so the two rules do not disagree. Narrowing the class signal as well
is reserved the same way this question was, and would be its own ticket.

ADR-0004 is `proposed`. The commit that closes this ticket moves it to
`accepted`, which is the practice ADR-0003 established.

The record's two new fields cost one word and one finding number per finding
line, and they buy the two facts the narrowed rule and its falsifier turn on.
Closed descriptions are not rewritten, so the fields are readable only from
rounds recorded after this ticket — which is also why the falsifier's second
arm counts only those rounds, and why its standing count is zero rather than
a number read from history.

Noticed and left, with its route already recorded: "The record." paragraph in
`docs/tier-review-model.md`, "When review ends", lists the per-round fields
only and has never listed the per-finding ones. EM-014-001's round-1 finding
R1.9 recorded that, outside its Files, "for whichever ticket next touches
that paragraph". This ticket does not touch it, and round 2's R2.5 is right
that the gap is one field wider than it was: the rank this change puts on
every finding line is another field that paragraph does not list, on top of
those it has not listed since EM-014-001 closed. The route is unchanged and
the finding goes to it — the paragraph is repaired by the ticket that next
touches it, a limit this repository already recorded rather than one this
ticket invents.

The template change is wider than the sentence the maintainer approved: a
rank on every finding line changes the record that every future critical-tier
review writes, not only the reviews of tickets that touch this rule. The
maintainer accepted it on 2026-09-07 on the condition that ADR-0004 state the
template change as a consequence of the narrowing and carry its cost, and
that is where it is stated — what changed, why the narrowing required it, and
a cost of about five words and five finding numbers per review record, from
the mean of 5.29 finding lines over the 34 rounds at 60f39fb read by the
counting command quoted in that record's Context with `f/n` printed as well,
run after f8880b5.

No child ticket was raised: nothing outside the amendment and its round-1
repair was found needing work.

### Review
| Round | Must-fix | Where (rules / lists / documents / tests) | Inside previous round's fix | Repaired by |
|---|---|---|---|---|
| 1 | 3 (of 8 findings) | documents: §6's narrowed trigger turned on a per-finding rank the record did not carry (must-fix); the falsifier's new second arm named evidence the record could not produce (must-fix); the template's flat prohibition forbade the line the class signal demands (must-fix); nothing obliges a reviewer to rank; ADR-0004's second arm without a standing count; the same template sentence prohibiting where §6 owes; the authority for narrowing the rule unnamed in ADR-0004; an ungrammatical carried-forward sentence blessed by the whole-bullet re-wrap | — | 8e87a58 |
| 2 | 2 (of 5 findings) | documents: the template's two finding-line exemplars fixed the rank as a literal, one per column, so the record's sole statement of its own form modelled rank as following column (must-fix); the same template exempted a note's repair from the class form except where the class signal had fired, unscoped in time, so every later note on that rule owed the form for the rest of the review (must-fix); §6 barring re-ranking but not renumbering or merging, which breaks the finding number the new field and the falsifier's second arm read; ADR-0004 crediting the narrowing with avoiding a separation-of-duties failure the narrowing created; "The record." in `docs/tier-review-model.md` one field further behind | 2 of 2 | f8880b5 |
| 3 | <n> | <where> | <m of n> | <commit> |

Round 3 pending — the cap. The total is derived from the rows and is not
asserted beside them.

**The class.** Round 1's three must-fixes were not three sentences to patch.
The question that produces them, asked of the whole change: **on what fields
of the record does this narrowing depend, and does the record carry them?**
Its siblings are enumerated in Falsification above, against the record at
60f39fb, together with the second class R1.3 belongs to and why the two were
not collapsed into one.

- R1.1 · permits · must-fix · §6, "a must-fix being a finding the reviewer
  records as blocking merge" · the reviewer ranks findings, but no record
  field carried a per-finding rank: the template's finding lines carried
  column, rule, remedy, cost and inside-previous-fix, and the table carried a
  per-round count plus "(must-fix)" in the prose of the Where cell, unlinked
  to R-numbers. The executor writes the description and transcribes both, and
  the only bar on reclassifying was scoped to condition 2 of "When review
  ends", so the party the control sits on could set the obligation's scope —
  remedy: a rank on the template's per-finding line, as recorded by the
  reviewer, with §6 saying the executor transcribes and does not re-rank;
  cost, as the reviewer measured it: one word per finding line, 180 findings
  over 34 rounds at 60f39fb, on a template this change already opens; inside
  previous fix: no
- R1.2 · permits · must-fix · the falsifier's new second arm · it named
  evidence the record does not carry: seeing "a repair made for a note draw a
  finding inside that repair" needs the identity and rank of the earlier
  finding, and the tables carried an aggregate "m of n" and a per-round count
  only, so the arm was unreadable except where the previous round had zero
  must-fixes, and no such pair exists in the 34 rounds at 60f39fb; the change
  also removed the note's repair line from the description, so the arm's
  population became unrecorded at the moment the arm was written — remedy:
  the linking field added, the inside-the-previous-fix field naming the
  finding whose repair a finding sits inside, and the arm restated on those
  fields and on rounds recorded under this rule; cost: one field per finding;
  inside previous fix: no
- R1.3 · permits · must-fix · `templates/PR-DESCRIPTION.md`, "A finding the
  reviewer did not record as a must-fix carries no line here" · flat, with no
  counterpart to §6's saving clause, so it forbade the line the class signal
  in "What a review reports" demands when a rule ping-pongs across two rounds
  on findings neither of which blocked merge — a control the maintainer did
  not narrow — remedy: §6's saving clause carried into the template; cost:
  one sentence; inside previous fix: no
- R1.4 · permits · note · §6, "A finding the reviewer did not record as a
  must-fix owes…" · silence defaults to exempt, since nothing obliges a
  reviewer to rank every finding — remedy: a sibling of R1.1's class; an
  unranked finding is now repaired at its class as a must-fix is, so silence
  cannot narrow the obligation and the executor gains nothing from a missing
  rank; inside previous fix: no
- R1.5 · permits · note · ADR-0004's second arm · no standing count, against
  this repository's practice ("the count was five", "already past twenty"),
  and the change itself named one instance, so the arm sat close to firing
  with no reader able to see it — remedy: the count stated, zero over zero
  rounds under this rule at 60f39fb, beside the eleven historical
  near-instances over the 34 rounds there and the method that found them;
  cost: one sentence, taken as three paragraphs because the count needed its
  population and its method; inside previous fix: no
- R1.6 · refuses · note · the same template sentence · "carries no line" is a
  prohibition where §6 says "owes", so an executor that asked the class
  question on a note and found siblings could not record them, though
  ADR-0004's own Neutral consequence says recording more costs nothing —
  remedy: "need carry no line", which is R1.3's sentence; a loosening;
  inside previous fix: no
- R1.7 · permits · note · ADR-0004, "Amendment in place rather than
  retirement" · bullet 4 of "Retiring a control" authorises widening the
  falsifier; bullet 3's amendment path is conditioned on a match being
  technical, which the record says did not occur, so the authority for
  narrowing the rule — the maintainer's §3 answer — went unnamed — remedy:
  the paragraph now names the authority for each half and says the third
  bullet is not it; cost: one clause, taken as a paragraph; inside previous
  fix: no
- R1.8 · refuses · note · §6's carried-forward sentence · "is recorded as the
  third condition … records a list" is ungrammatical, pre-existing, and the
  whole-bullet re-wrap at 3258933 had blessed it inside ADR-0004's "text that
  replaces it" block — remedy: "is recorded the way the third condition …
  records a list", repaired in §6 and in that block, with nothing else in
  either re-flowed; inside previous fix: no

No condition of "When review ends" was met by round 1: it found must-fixes,
none of them inside a limit the ticket records, and none adding an entry to
an enumeration. Round 1 of a cap of three. The class signal did not fire —
one round, so no first-column finding has a next-round second-column finding
inside its fix.

Post-review tree check after round 1: `git status --porcelain` empty, `git
worktree list` showing only worktrees this ticket's executor did not create.

**The class signal fired, on R2.2.** R1.3 was a first-column finding on the
template sentence that says which repairs owe a class line; R2.2 is a
second-column finding on that same sentence, inside R1.3's fix. That is the
both-columns-on-one-rule signal in "What a review reports", read from the two
fields every finding line carries — the column, and the finding whose repair
it sits inside — and it asks for a redesign against the class rather than a
further adjustment. Beside the signal the reviewer recorded the adjustment it
would otherwise have proposed: scope the exception to the round the signal
fired in. **That adjustment was refused, and the redesign taken instead.**
Taken, it would have left an exception bolted onto a prohibition with a scope
written by hand, and the next rule wanting the class form would have arrived
as a third clause needing a scope of its own — which is the class, and not
the missing scope.

**What the redesign removed.** The exception. The template no longer says
which repairs owe a class line by exempting a note's repair and then carving
the class signal back out of the exemption. It says a line is owed wherever a
rule asks for the class form, and that each such rule says which repairs it
asks it of: the contributor policy's §6 asks it of a repaired must-fix and of
the repair of a finding the reviewer left unranked; the class signal asks it
of the round's repair of the rule the signal fired on. A note's repair owes no
line because §6 does not reach it and no other rule asks — not because a
clause exempts it. Three things follow. The temporal scope R2.2 found missing
is now the class signal's own words, "the round's repair of that rule", and
cannot drift from them, because the template quotes no trigger to drift. A
rule that later asks for the form asks by asking, and needs no amendment
there. And a reader deciding whether a finding's repair owes a line reads the
rules in force rather than the history of amendments to one sentence. What did
not change: §6's reach, the class signal's trigger, and what a line contains.
Cost: the statement runs 23 lines where the sentence it replaces ran 11, from
`git show 24d81a8:templates/PR-DESCRIPTION.md | sed -n '/^For each review
must-fix repaired/,/^claim.$/p' | wc -l` and `sed -n '/^For each repair a line
here/,/costs a later reader nothing.$/p' templates/PR-DESCRIPTION.md | wc -l`,
both run after f8880b5; twelve lines in a template, paid once, where a scoped
exception would have been paid again by every rule added after it.

- R2.1 · permits · must-fix · `templates/PR-DESCRIPTION.md`, the two Review
  finding-line exemplars · rank is the only field written as a literal where
  every other is a placeholder, and it reads `permits · must-fix` on one line
  and `refuses · note` on the other — so the record's sole statement of its
  own form models rank as determined by column, which "What a review reports"
  forbids ("whether a finding blocks merge does not depend on its column") and
  whose falsifier is exactly "second-column findings … all notes and never
  must-fixes"; the second line also fixes `inside previous fix: no` as a
  literal where the first carries the placeholder — remedy: `<rank>` and the
  full placeholder on both lines, with the prose above them naming the two
  values and saying the column does not settle them; cost: none, it tightens
  nothing; inside previous fix: R1.1
- R2.2 · refuses · must-fix · the same template, "except where the class
  signal … has fired on the rule it landed on" · unscoped in time: once the
  signal fires on a rule, every later note on that rule owes class, siblings
  and a red count for the rest of the review, though the model asks the form
  only of "the round's repair of that rule" — remedy: the redesign recorded
  above, which states which repairs owe a line by naming the rules that ask
  for the form; the adjustment the reviewer recorded beside the signal,
  scoping the exception to the round the signal fired in, was refused; cost:
  none beyond the twelve lines counted above — the redesign asks nothing that
  §6 and the class signal do not ask themselves; inside previous fix: R1.3.
  **The class signal fired here**, and the redesign is what it asks for.
- R2.3 · permits · note · §6, "transcribes both and does not re-rank" · bars
  re-ranking only; renumbering or merging findings breaks the R-number the new
  field and the arm depend on — remedy: "does not re-rank, renumber or merge",
  in §6, in the same sentence of `templates/PR-DESCRIPTION.md`, and in
  ADR-0004's quotation of §6, so the three do not diverge, with the reason
  stated once and a clause saying that naming several findings in one repair
  line is not a merge; cost: the reviewer priced three words and this is two
  sentences; an executor that would have tidied the reviewer's numbering may
  not, and nothing recorded pays it — of the 46 repair lines in
  `docs/tickets/done/` at 60f39fb, three answer for several findings at once
  and each names every number, from `grep -rh "^- R[0-9]"
  docs/tickets/done/*.md | wc -l` and the same grep piped to `grep -cvE "^-
  R[0-9]+\.[0-9]+ "`, run after f8880b5 on a directory this branch does not
  touch; inside previous fix: R1.1
- R2.4 · permits · note · ADR-0004 Decision, "the separation-of-duties
  failure the narrowing exists to avoid" · the narrowing created it; the
  repair closes it — remedy: reworded, so the record says the narrowing opened
  the scope-setting the rank field closes rather than crediting it with
  avoiding a failure it introduced; inside previous fix: R1.1
- R2.5 · permits · note · `docs/tier-review-model.md`, "The record." · one
  field further behind — routed to R1.9's recorded limit — remedy: the Risks
  paragraph above no longer says the paragraph is no more behind than before;
  it names the rank as the field that widened the gap and routes it, unchanged
  and unrepaired here, to the limit EM-014-001's round-1 finding R1.9 recorded
  for whichever ticket next touches that paragraph; inside previous fix: R1.1

No condition of "When review ends" was met by round 2. It found must-fixes;
neither lies inside a limit this ticket records, since round 1 brought the
template's finding-line form into this ticket's scope and both must-fixes are
new in round 1's repair; and neither adds an entry to an enumeration
maintained against an adversary. Round 2 of a cap of three: if round 3 records
a must-fix, the ticket blocks to the maintainer with this record attached.

Post-review tree check after round 2, made before the first edit of the round:
`git status --porcelain` empty, `git worktree list` showing only worktrees
this ticket's executor did not create.
