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
where the change has no suite.

The exemption is from that bullet only. The class signal in "What a review
reports" asks for the same form on a trigger of its own — a first-column
finding on a rule followed in the next round by a second-column finding
inside the previous fix — and this decision does not reach it. Narrowing
that control is a decision reserved the same way, and what the maintainer
narrowed is §6.

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
  which this narrowing does not reach. A class with no finite enumeration —
  "what could a user type" — is recorded as the third condition of "When
  review ends" in `docs/tier-review-model.md` records a list: best-effort,
  with the coverage stated. Where the change has no suite, each sibling says
  what a reader would do differently, as the template says for a claim. The
  form is in `templates/PR-DESCRIPTION.md`, and the reason a test pins a claim
  rather than a mechanism is with the gate in `docs/quality-gates.md`.
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
  suite run per sibling and prevents nothing — or a repair made for a finding
  the reviewer did not record as a must-fix draws a finding inside that repair
  in a later round, more than once over a stated population of closed tickets,
  which is the exemption above costing the rounds the enumeration exists to
  save. The second arm is read from the Review tables of closed critical-tier
  tickets, which record each round's findings, which of them blocked merge,
  and how many sat inside the previous round's fix.
```

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

## Consequences

- **Positive:** the obligation is charged on the population EM-009 priced.
  At 60f39fb the rule as it stood reached the 180 findings counted above;
  narrowed, it reaches 40.
- **Positive:** "repair of the instance" is written where a reviewer has
  said the merge is blocked, so the claim the phrase makes is one someone is
  already checking in the next round.
- **Negative:** a note repaired one branch too shallow is now exempt, which
  is the defect EM-009 was raised for. It is not hypothetical: round 2 of
  EM-009's own review found one. Round 1's repair of R1.6 — a note, the exit
  for a class with no finite enumeration — named "the stopping rule" without
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
the obligation agree. No closed pull-request description is rewritten, and
no rule leaves a document. Nothing else states the obligation's trigger:
`docs/quality-gates.md` and `docs/tier-review-model.md` point at §6 rather
than restating it.
