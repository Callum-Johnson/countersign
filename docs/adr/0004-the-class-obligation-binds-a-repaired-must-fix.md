# ADR-0004: The class obligation binds a repaired must-fix, not a note

- **Status:** proposed
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
the party the obligation sits on could have set its scope — the separation-of-duties failure the
narrowing exists to avoid. So each finding line in
`templates/PR-DESCRIPTION.md` now carries the rank the reviewer gave the
finding, and its inside-the-previous-fix field names the finding whose
repair it sits inside rather than answering yes or no. The reviewer records
both; the executor transcribes them and does not re-rank; a finding the
reviewer left unranked is repaired at its class as a must-fix is, so silence
cannot narrow the obligation either. The class signal in "What a review
reports" reads the same two fields it always did — the column, and whether
the finding sits inside the previous fix — and is unchanged by the addition.

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
  and, where the finding sits inside the previous round's fix, which finding's
  repair it sits inside — the two facts this bullet and its falsifier turn on,
  in the form `templates/PR-DESCRIPTION.md` gives. The executor transcribes
  both and does not re-rank, exactly as it routes a finding under the second
  condition of "When review ends" without reclassifying it; a rank the
  executor can set is a scope the controlled party can set. A finding the
  reviewer left unranked is repaired at its class as a must-fix is, so that
  silence never narrows the obligation of the party writing the description.
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
  carries its rank and, where it sits inside the previous round's fix, the
  finding whose repair it sits inside; it counts only rounds recorded under
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
- **Negative:** every finding line costs one more word for the rank, and its
  inside-the-previous-fix field costs a finding number where it cost `yes`.
  At 60f39fb that is 180 findings over 34 rounds, on records already
  written and not rewritten; the cost falls on rounds recorded from here.
  It buys the two facts the narrowed rule and its falsifier turn on.
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
into the finding whose repair the finding sits inside. The form is stated
in that template alone: nothing under `docs/` restates it, and the tier
review model's own use of it — the column and whether the finding sits
inside the previous fix, for the class signal — is satisfied unchanged. No closed pull-request description is rewritten, and
no rule leaves a document. Nothing else states the obligation's trigger:
`docs/quality-gates.md` and `docs/tier-review-model.md` point at §6 rather
than restating it.
