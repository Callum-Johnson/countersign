# ADR-0005: The class obligation binds a repaired must-fix, not a note

- **Status:** accepted
- **Date:** 2026-09-07
- **Deciders:** maintainer, answering the question EM-009-001 reserved to
  the maintainer under the contributor policy's §3
- **Related:** EM-009-001 (this decision); EM-009 (the rule amended, and its
  round-1 finding R1.7); ADR-0003 (every rule states its falsifier, and a
  control can be retired or amended in place); `docs/tier-review-model.md`,
  "Retiring a control"; `docs/ai-contributor-policy.md`, §6

## Context

EM-009 added the class obligation to the contributor policy's §6: a review
finding is repaired at its class, and the description names the class, the
siblings that question enumerates, and a red count per sibling — or says
**repair of the instance**, in those words. As landed, the rule bound "each
finding repaired".

EM-009's own Costs section priced it on must-fixes: on OMN-021's 46
must-fixes, an assumed three siblings each, about 138 suite runs. Nothing in
the rule distinguished a must-fix from a note, so the rule charged a
population the ticket that introduced it never counted.

The independent review of EM-009 found that and recorded it as a
second-column finding, R1.7, rather than repairing it:

> R1.7 · refuses · the class obligation · it binds notes as well as
> must-fixes, and the ticket priced it on must-fixes; on this repository's
> four closed records at 0781e98 that is 55 findings against 5 must-fixes,
> per the reviewer's count of their Review tables — recorded, not fixed,
> since the Behaviour says "each review finding"; the maintainer may narrow
> it by a retirement ticket.

The record has grown since. Over the 34 review rounds in this repository's
closed tickets at 60f39fb whose rows state both counts, the Review tables
record 40 must-fixes against 180 findings, read by:

```sh
grep -rh "^| [0-9] | [0-9]* (of [0-9]" docs/tickets/done/*.md \
  | sed -E 's/^\| [0-9]+ \| ([0-9]+) \(of ([0-9]+).*/\1 \2/' \
  | awk '{m+=$1; f+=$2; n++} END {print n, m, f}'
```

Three further rounds, in EM-019-001-001, state a must-fix count without a
finding count and are outside those figures.

What the wider population bought is measurable, and it is nothing. Four
closed tickets record repairs in §6's form — EM-009, EM-016, EM-019-001 and
EM-019-001-001 — whose repair lines are listed by `grep -rn "^- R[0-9]"
docs/tickets/done/*.md`, and whose must-fix status is read from each
ticket's own Review row. Twelve of those repairs are of findings the round
did not record as must-fixes, and all twelve declare "repair of the
instance" with no siblings enumerated. Six lines name a class, covering
seven findings, and every one of the seven is a must-fix. No repair of a
note has ever named a class in this repository.

Two of the three answers EM-009-001 set out narrow a control that sits on
the executor, and "Separation of duties" is explicit that the party subject
to a control does not get to remove it. The executor blocked under §3
rather than choosing, and the question stood until the maintainer answered
it on 2026-09-07.

## Decision

The class obligation in `docs/ai-contributor-policy.md`, §6 binds **a
repaired must-fix** — a finding the reviewer records as blocking merge, as
"When review ends" in `docs/tier-review-model.md` defines it. **A note
carries nothing**: a finding the reviewer did not record as a must-fix owes
neither a class and its siblings nor the words "repair of the instance",
whether it is repaired in the round or at close.

Everything else the obligation asks is unchanged — the class, the siblings,
the test and red count per sibling, the "repair of the instance" wording,
the exit for a class with no finite enumeration, and what a sibling records
where the change has no suite. What changes beside the trigger is the
record's own form, stated two paragraphs below.

The exemption is from that bullet only. The class signal in "What a review
reports" asks for the same form on a trigger of its own — a first-column
finding on a rule followed in the next round by a second-column finding
inside the previous fix — and this decision does not reach it. Narrowing
that control is a decision reserved the same way, and what the maintainer
narrowed is §6.

**The record carries the rank.** The narrowing turns on a fact the record
did not carry: which findings the reviewer recorded as blocking merge,
finding by finding. The Review tables carried a per-round must-fix count and
"(must-fix)" in the prose of the Where cell, tied to no numbered finding,
while the finding lines carried the column, the rule, the remedy, the cost
and whether the finding sat inside the previous round's fix. The executor
writes the description and transcribes the reviewer's findings into it, so
the party the obligation sits on could have set its scope. The narrowing
opened that: before it the rank decided nothing, and after it the rank
decides how much a repair must justify itself, which is the
separation-of-duties failure this record closes rather than one it avoided.
So each finding line in `templates/PR-DESCRIPTION.md` now carries the rank
the reviewer gave the finding, and its inside-the-previous-fix field names
the finding whose repair it sits inside rather than answering yes or no. The
reviewer records both; the executor transcribes them and does not re-rank,
renumber or merge; a finding the reviewer left unranked is repaired at its
class as a must-fix is, so silence cannot narrow the obligation either. The
class signal in "What a review reports" reads the same two fields it always
did — the column, and whether the finding sits inside the previous fix — and
its trigger is untouched; which values of the second field it can read is
settled in the paragraph below.

**Both fields carry every state their rules name.** A field that cannot hold
a state one of its readers names is the defect the paragraph below states —
a rule whose trigger the record does not carry can be neither checked nor
retired — and that defect in the record's own form would be the narrowing
paying for itself with an unreadable falsifier. So the rank takes three
values and not two: `must-fix`, `note`, and `unranked` where the reviewer
gave none, which §6 repairs at its class as it repairs a must-fix. The
inside-the-previous-fix field names a finding from any earlier round and not
only the round before, because the falsifier's second arm counts a finding in
any later round while every other rule that reads the field asks about the
round before, and the finding's number says which round it came from; the
four rules that read it are listed once, in `templates/PR-DESCRIPTION.md`, so
that no second list of them can drift from the first. Where the reviewer
records that a finding sits inside an earlier fix without saying which the
field carries that, and where the reviewer writes something else again it
carries the reviewer's words: only a line naming a finding, or reading `no`,
is countable by any of the four, since the second arm needs the earlier
finding's rank and the other three need the round, which only the number
gives. The executor supplies neither a rank nor a finding number the reviewer
left out, for the reason the rank is the reviewer's at all. What a finding
line costs is unchanged — `unranked` is one word where `note` is one word,
and a finding number replaces `no` in the same field — and what the round
table costs is one count per row, of the must-fix lines the countability
sentence leaves uncountable, and which so sit neither in its `m of n` cell
nor out of it.

**The template change is a consequence of this narrowing, and it is wider
than the sentence amended.** A rank on every finding line changes the record
that every future critical-tier review writes, not only the reviews of
tickets that touch this rule. The maintainer accepted it on 2026-09-07, on
the condition that this record state why the narrowing required it and what
it costs, so that a later reader finds the reason here rather than an
unexplained extra field. Required, because the narrowed rule's trigger and
both arms of its falsifier are per-finding facts — the reviewer's rank, and
the finding whose repair a later finding sits inside — and a rule whose
trigger the record does not carry can be neither checked nor retired.
Without the field the only statement of a rank is the executor's prose, and
the executor is the party the obligation sits on: the narrowing would hand
it the scope it was narrowed to define. What it costs is one word and one
finding number per finding line, and one further number on each round row.
At 60f39fb the closed records hold 180 findings over 34 rounds, a mean of
5.29 finding lines per round, read from the counting command in Context
above with `f/n` printed as well — so about five words and five finding
numbers per review record, plus one number per round row, paid from here by
every critical-tier review.

The rule's text as it stood:

```
- A review finding is repaired at its class. For each finding repaired, the
  description names **the class** — the question which, asked of the whole
  change, produces this finding and its siblings: "what does the interpreter
  load" is a class, "`.py` files at the root" is an instance — and **the
  siblings** that question enumerates, each with the test that pins it and the
  count of tests that go red under its wrong implementation, one case per
  rival as the gate already requires. A repair that names no class says
  **repair of the instance**, in those words. That is permitted — some
  findings are singular — and it is a claim the reviewer can check: the next
  round finding a sibling is then a finding against the repair's own claim. A
  class with no finite enumeration — "what could a user type" — is recorded as
  the third condition of "When review ends" in `docs/tier-review-model.md`
  records a list: best-effort, with the coverage stated. Where the change has
  no suite, each sibling says what a reader would do differently, as the
  template says for a claim. The form is in `templates/PR-DESCRIPTION.md`, and
  the reason a test pins a claim rather than a mechanism is with the gate in
  `docs/quality-gates.md`.
```

The text that replaces it:

```
- A review must-fix is repaired at its class — a must-fix being a finding the
  reviewer records as blocking merge, as "When review ends" in
  `docs/tier-review-model.md` defines it. For each must-fix repaired, the
  description names **the class** — the question which, asked of the whole
  change, produces this finding and its siblings: "what does the interpreter
  load" is a class, "`.py` files at the root" is an instance — and **the
  siblings** that question enumerates, each with the test that pins it and the
  count of tests that go red under its wrong implementation, one case per
  rival as the gate already requires. A repair that names no class says
  **repair of the instance**, in those words. That is permitted — some
  findings are singular — and it is a claim the reviewer can check: the next
  round finding a sibling is then a finding against the repair's own claim.
  **A note carries nothing.** A finding the reviewer did not record as a
  must-fix owes neither a class and its siblings nor the words "repair of the
  instance", whether it is repaired in the round or at close. That exemption
  is from this bullet only; the class signal in `docs/tier-review-model.md`,
  "What a review reports", asks for the same form on a trigger of its own,
  which this narrowing does not reach. **The rank is the reviewer's, and the
  record carries it finding by finding.** Every finding line in the Review
  section says whether the reviewer recorded that finding as blocking merge
  and, where the finding sits inside the repair of a finding from an earlier
  round, which finding's repair it sits inside — the two facts this bullet and
  its falsifier turn on, in the form `templates/PR-DESCRIPTION.md` gives. An
  earlier round and not only the round before, because the falsifier's second
  arm counts a finding in any later round where every other rule that reads
  the field asks about the round before, and the finding's own number says
  which round it came from, so one field answers them all. Which rules read
  it is listed once, in `templates/PR-DESCRIPTION.md`, so that no second list
  of them can drift from the first. The executor transcribes both and does not
  re-rank, renumber or merge, exactly as it routes a finding under the second
  condition of "When review ends" without reclassifying it; a rank the
  executor can set is a scope the controlled party can set, and an R-number
  the executor can change is the link the falsifier's second arm and the
  inside-the-previous-fix field both read. Naming several findings in one
  repair line is not a merge: the numbers are all there. A finding the
  reviewer left unranked is repaired at its class as a must-fix is, so that
  silence never narrows the obligation of the party writing the description.
  **An absence is recorded as an absence.** The line says the rank was not
  given rather than carrying one the reviewer did not give, and says that a
  finding sits inside an earlier fix the reviewer did not identify rather than
  naming one; a value the executor supplies where the reviewer was silent is a
  value the party the obligation sits on has set. **A line is countable where it names a
  finding, reads `no`, or names the round the earlier fix sits in — `yes,
  round 3`.** A line naming the round answers every reader that needs only
  the round; it is not counted by the second arm alone, which needs the
  earlier finding's rank and so its identity. Any other value the reviewer
  wrote — `yes, unnamed`, or a hedge such as `partly` — is counted by none of
  the rules that read the field. Such a line is reported and left as it was
  written — the cost of the silence, and not something the description may
  resolve. This sentence is the one statement of which lines are countable;
  the rules and counts that read the field name it rather than restating the
  list.
  A class with no finite enumeration — "what could a user type" — is recorded
  the way the third condition of "When review ends" in
  `docs/tier-review-model.md` records a list: best-effort, with the coverage
  stated. Where the change has no suite, each sibling says what a reader would
  do differently, as the template says for a claim. The form is in
  `templates/PR-DESCRIPTION.md`, and the reason a test pins a claim rather
  than a mechanism is with the gate in `docs/quality-gates.md`.
```

The falsifier as it stood:

```
  **Retired when:** over a stated population of critical-tier tickets, repairs
  declared "repair of the instance" draw a sibling finding in the next round
  no more often than repairs that named a class; the enumeration then costs a
  suite run per sibling and prevents nothing.
```

The falsifier that replaces it, its second arm added by this decision:

```
  **Retired when:** over a stated population of critical-tier tickets, repairs
  declared "repair of the instance" draw a sibling finding in the next round
  no more often than repairs that named a class — the enumeration then costs a
  suite run per sibling and prevents nothing — or a finding in a later round
  sits inside the repair of a finding the reviewer ranked a note, more than
  once over a stated population of closed tickets, which is the exemption
  above costing the rounds the enumeration exists to save. The second arm is
  read from the finding lines of closed critical-tier tickets, each of which
  carries its rank and, where it sits inside the repair of a finding from an
  earlier round, that finding; it counts only rounds recorded under
  this rule, since a note repaired while the obligation still bound it is not
  evidence about the exemption.
```

**The second arm's standing count is zero, and what it is zero over.** The
arm counts a finding in a later round whose line names, as the fix it sits
inside, a finding its own line ranks a note. It counts only rounds recorded
under this amendment, because a note repaired while the obligation still
bound it carried the class question already and so says nothing about the
exemption. No such round exists at 60f39fb: the count is zero over zero
rounds, and the first ticket closed under this rule starts it.

**Beside it goes the count the arm cannot reach.** A finding line whose
inside-the-previous-fix field the countability sentence leaves uncountable is
countable by none of that field's four readers, and a standing zero reported without it would let a
starved arm read as a quiet one — the unnamed answer is the cheap one, and
the party that gains from the arm never firing is the party writing the
record. So both counts are stated, and both are zero over zero rounds
recorded under this amendment. The record as it stood is what makes the
second count worth reporting: of the 5 finding lines carrying that field in
`docs/tickets/done/` at 60f39fb, 1 names a finding or reads `no` and 4 do
not — one bare `yes`, two `yes` with commit hashes, and one `partly` — from
`grep -rh "inside previous fix" docs/tickets/done/*.md | wc -l` and the same
grep piped to `grep -cE "inside previous fix: (no|R[0-9]+[.][0-9]+)"`, run
at that commit on a directory EM-009-001's branch does not touch. Those five
predate the field's present form and none was written under this rule, so
they measure how often a reviewer answers without naming and not how often
the arm will be starved.

The pattern the arm watches for was not rare under the rule as it stood.
Over the 34 rounds recorded at 60f39fb, eleven findings in a round after the
first sit inside the repair of a finding their round did not record as
blocking merge: two in EM-006's round 2, on its round-1 findings 5 and 10;
one each in EM-006-001 on R1.2, EM-007 on its note 7, EM-009 on R1.6,
EM-012 on R1.6, EM-014-001 on R1.7, EM-016 on R1.9 and EM-019-001-001 on
R2.2; and two in EM-021's round 2, on R1.5 and R1.13. No command produces
that figure. It was obtained by reading every round after the first for the
prose naming the earlier finding or remedy the later finding sits inside,
and reading that earlier finding's rank from its own round's Where cell —
seven of the eleven named outright by the record, four matched from the
remedy that introduced the text. It is a floor: three rounds — EM-010's
round 2, EM-016's round 3 and EM-020's round 2 — record that a finding sat
inside the previous fix without naming which, and cannot be attributed at
all. That reading is the labour the rank and inside-which fields remove, and
its incompleteness is why they were added rather than the arm being stated
on the fields the record already had.

Those eleven are not evidence against this decision. Every one of them
happened while the obligation bound notes, and every note repaired in this
repository under it declared "repair of the instance" and named no class. So
they measure what the obligation on notes prevented, which is nothing — the
maintainer's reason for narrowing — and the arm has to run forward from
repairs that carried nothing to say anything about the exemption itself.

## Rationale

The obligation was added so that a repair is made at the level of the
question that produced the finding, rather than one branch too shallow. On
notes it produced no such repair: twelve note repairs, twelve declarations
of "repair of the instance", no class named. A declaration written every
time without the question being asked is the decorative claim ADR-0003
exists to remove — the same defect as a falsifier written to satisfy a
section, or a test with a zero red count. Charging the obligation on 180
findings to collect it on 40 trains the phrase and not the question.

R1.7 did not match the rule's stated falsifier, and "Retiring a control"
says a second-column finding that does not match is a finding against the
falsifier as much as against the rule. That is why this amendment widens
the falsifier as well as narrowing the rule. Why the finding was not
foreseen: the falsifier EM-009 wrote asks whether the enumeration catches
siblings that "repair of the instance" missed, and it takes the population
the rule reaches as given, so no evidence gathered under it could ever have
shown that population was the wrong one. The second arm names evidence in
the direction this decision moves the rule.

Amendment in place rather than retirement, because what changed is the
population the rule reaches and not the rule: the class, the siblings and
the per-sibling count are the same obligation, charged where the reviewer
has said the merge is blocked. "Retiring a control" makes the record the
control and not the removal, and this record carries the old text, the
finding, and the new text.

The two halves of the amendment rest on different authority, and neither on
the other's. Widening the falsifier is authorised by that section's fourth
bullet: R1.7 did not match the falsifier EM-009 wrote, which makes it a
finding against the falsifier, widened by the ticket the finding raises as
an amendment with record. Narrowing the rule is not authorised there. The
section's third bullet — amendment in place where the match was technical
and the correction small — is conditioned on a match, and R1.7 matched
nothing, as the paragraph above says. The authority for the narrowing is the
maintainer's answer to the question EM-009-001 reserved under the
contributor policy's §3, given on 2026-09-07 and recorded in that ticket;
"Separation of duties" is why it had to come from there and not from the
executor. This paragraph says why the amendment keeps the rule in place; it
does not supply the permission to change what the rule reaches.

## Consequences

- **Positive:** the obligation is charged on the population EM-009 priced.
  At 60f39fb the rule as it stood reached the 180 findings counted above;
  narrowed, it reaches 40.
- **Positive:** "repair of the instance" is written where a reviewer has
  said the merge is blocked, so the claim the phrase makes is one someone is
  already checking in the next round.
- **Positive:** the falsifier's second arm can be read from the record. A
  reader asking what would make it fire looks at the finding lines in the
  Review section of each closed critical-tier ticket, and counts the lines
  whose inside-the-previous-fix field names a finding whose own line is
  ranked `note`. Two such lines, in rounds recorded under this rule, retire
  the exemption. Before this decision the arm named the rank of a finding
  and the identity of the fix it sat inside, and the record carried neither.
  A line the countability sentence leaves uncountable — `yes, unnamed`, or
  whatever else the reviewer wrote that neither names a finding, reads `no`,
  nor names the round — is one no reader of the field can count, and it says so
  on its face rather than passing as a `no`; the round table reports how
  many such lines a round holds, and this record states their standing count
  beside the arm's own.
- **Negative:** every finding line costs one more word for the rank, and its
  inside-the-previous-fix field costs a finding number where it cost `yes`.
  At 60f39fb that is 180 findings over 34 rounds, a mean of 5.29 finding
  lines per round, on records already written and not rewritten; the cost
  falls on rounds recorded from here, and on every critical-tier review from
  here rather than only on the tickets that touch this rule. Each round row
  costs one number besides — the count of must-fix lines the countability
  sentence leaves uncountable, written even when it is zero. It buys the two facts the narrowed rule and
  its falsifier turn on.
- **Negative:** a note repaired one branch too shallow is now exempt, which
  is the defect EM-009 was raised for. It is not hypothetical, and the count
  is in the standing-count paragraph above: eleven times over the 34 rounds
  at 60f39fb, a finding in a later round sat inside the repair of a finding
  its round did not record as blocking merge. The clearest is round 2 of
  EM-009's own review. Round 1's repair of R1.6 — a note, the exit for a
  class with no finite enumeration — named "the stopping rule" without
  saying where it is, a section name no document carries. Under this
  decision that repair would have carried nothing. The maintainer accepted
  the risk, and the falsifier's second arm is where the evidence goes if it
  recurs.
- **Negative:** the reviewer's must-fix call now decides how much a repair
  must justify itself, so a finding recorded as a note is cheaper to repair
  than one recorded as blocking merge. The reviewer makes that call and the
  executor does not, which is what makes the asymmetry acceptable.
- **Neutral:** the class signal in "What a review reports" keeps its own
  trigger, so a rule ping-ponging across two rounds still draws the class
  form whether or not either finding blocked merge.
- **Neutral:** descriptions closed under the wider rule are not rewritten.
  They record more than the rule now asks, which costs a later reader
  nothing.

## Alternatives considered

### Alternative 1: Leave the obligation binding every repaired finding

The rule as EM-009 landed it. Rejected by the maintainer on the evidence
above: on every note repaired in this repository the obligation produced the
words "repair of the instance" and no class, which is the declaration
written by habit rather than the question asked. Its cost is real — a class
question on a wording note rarely has siblings — and its yield in the record
is zero.

### Alternative 2: Narrow by round

A note repaired in the same commit as the round's must-fixes is covered by
the must-fix's class statement and carries nothing of its own. Rejected: it
makes the obligation depend on how the executor packages commits, which the
executor chooses, so the party subject to the control would set its own
scope. The must-fix line is drawn by the reviewer instead.

## Migration

EM-009-001 amends §6 and the matching paragraph of
`templates/PR-DESCRIPTION.md` in one commit, so that the two descriptions of
the obligation agree, and the same commit adds the rank to that template's
finding-line form and turns its inside-the-previous-fix field from a yes/no
into the finding whose repair the finding sits inside, in any earlier round.
That template carries the only list of the four rules that read the field, so
that no second list of them can drift from it, and the round table's count of
the must-fix lines that sentence leaves uncountable.
The same template carries §6's three forms of a repair line — a class with
its siblings, a class with no finite enumeration recorded best-effort with
its coverage stated, and the words "repair of the instance" — so that the
record's form holds every state the rule names. The form is stated
in that template alone: nothing under `docs/` restates it, and the tier
review model's own use of it — the column and whether the finding sits
inside the previous fix, for the class signal — is satisfied unchanged. That
template says which repairs owe a class line by naming the rules that ask
for the form, §6 and the class signal, and not by listing exceptions to a
prohibition, so a rule that later asks for the form needs no amendment
there. No closed pull-request description is rewritten, and
no rule leaves a document. Nothing else states the obligation's trigger:
`docs/quality-gates.md` and `docs/tier-review-model.md` point at §6 rather
than restating it.
