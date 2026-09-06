---
id: EM-009-001
title: The class obligation binds every repaired finding and was priced on must-fixes
status: blocked
tier: critical
complexity: S
dependencies: []
claimed_by: claude-fable-5-1
claimed_at: 2026-09-06
blocked_at: 2026-09-06
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

## PR Description

> Leave this section empty when authoring the ticket.
