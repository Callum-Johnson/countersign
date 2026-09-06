---
id: EM-019-001-001
title: Rule-adding tickets produce no decision record, against the trigger list
status: in-progress
tier: critical
complexity: S
dependencies: []
claimed_by: claude-fable-5-1
claimed_at: 2026-09-06
---

# EM-019-001-001 — Rule-adding tickets produce no decision record

## Context

Raised by the independent review of EM-019-001 (finding R1.6 of round 1).

`docs/adr-process.md` lists "A workflow rule changes" as a trigger for a
decision record, and gives the test: "if the decision affects multiple
tickets or constrains future work, it is an ADR". Five tickets closed in
this repository add a rule to a process document and produce no record —
EM-008, EM-009, EM-010, EM-011, EM-012 — and EM-016 and EM-019-001 add one
each. The repository holds three decision records, all of them decisions
*about* the process rather than rules within it.

Either the trigger means something narrower than it says, or the practice
has been wrong seven times. Nothing written down says which, so a
contributor reading the trigger list cannot tell whether their rule-adding
ticket owes a record.

## Specification

Documentation change only.

### Files

- `docs/adr-process.md` — "When to write one".

### Public surface

N/A — this repository publishes documents. One trigger is made precise.

### Behaviour

- The trigger says what "a workflow rule changes" reaches: a decision that
  changes how the process itself is governed, as against a rule added
  inside a document under an existing decision. The practice this
  repository has followed is the second, and the document says so.
- Where the line falls is stated with an example on each side: ADR-0003
  (the falsifier obligation, which changed how every rule is written) on
  one, and EM-011's review-isolation rule (added under the existing review
  model) on the other.
- **The falsifier of the line this ticket draws:** retired when a rule
  added under an existing decision, and therefore recorded nowhere, is
  found to have been undone or contradicted by a later contributor who
  could not see why it was there, more than once over a stated population
  of merged changes. The line is then drawn too narrowly and the trigger
  should reach those rules after all.

## Acceptance criteria

1. AC1: `docs/adr-process.md` states what "a workflow rule changes"
   reaches, with an example on each side of the line.
2. AC2: The seven rule-adding tickets that produced no record are either
   consistent with the stated line, or named in the pull-request
   description as a gap the decision accepts.
3. AC3: The line this ticket draws carries its own **Retired when:**
   line, distinct from the one the trigger list already has at baseline.
4. AC4: An independent agent reviews this and records findings in two
   columns.

## Out of scope

- Writing decision records retrospectively for the seven. If the answer is
  that they owed one, that is a separate ticket, and ADR-0001's rejection
  of backdating applies to how it is done.
- Any other trigger in the list.

## References

- `docs/adr-process.md`, "When to write one".
- EM-008, EM-009, EM-010, EM-011, EM-012, EM-016, EM-019-001 — the
  rule-adding tickets that produced no record.
- ADR-0003 — the one rule-level decision that did.

## Notes

Proposed `critical`: `docs/adr-process.md` is a process document, which
ADR-0002 classifies as process-surface, and an author may raise but never
lower. EM-007-002 owns whether that classification is right; until it is
answered, the tier that does not remove a control is the one to propose.

## PR Description

### Ticket
EM-019-001-001 — Rule-adding tickets produce no decision record, against the
trigger list

### Tier
critical — `docs/adr-process.md` is a process document, process-surface under
the operative test's fifth clause and ADR-0002. Independent review is
available in ADR-0002's sense and is recorded below.

### Summary
`docs/adr-process.md`, "When to write one", now states what "a workflow rule
changes" reaches: a decision that changes how the process itself is governed,
and a rule retired or amended under "Retiring a control"; not a rule added
inside a document under an existing decision, whose ticket is its record.
ADR-0003 is the example on the first side and EM-011's review-isolation rule
on the second, the document says this is the practice the repository has
followed, and the line carries its own **Retired when:**.

**Second-instance bar.** This ticket was raised before EM-021 closed, so the
bar's "not ready" clause in `docs/tier-review-model.md`, "A rule needs a
second instance", does not bind it. Its Context nonetheless names seven
instances — EM-008, EM-009, EM-010, EM-011, EM-012, EM-016 and EM-019-001 —
each a rule added with no record, on this repository, and all seven are
readable in `docs/tickets/done/`. It was raised after EM-014 closed, so it is
not among ADR-0003's exempt tickets, and it states the falsifier of the line
it draws in its Behaviour, as "Who this binds" requires.

### Acceptance criteria
- [x] AC1: `docs/adr-process.md` states what "a workflow rule changes"
  reaches, with an example on each side of the line — see the paragraph
  beginning **What "a workflow rule changes" reaches** in "When to write
  one", at f51ad72. ADR-0003 is named on the reaching side, with why no
  document could have carried it as one rule among the others; EM-011's
  rule, `docs/quality-gates.md`, "Review isolation", is named on the other,
  with the decision it sits under (ADR-0002).
- [x] AC2: each of the seven tickets checked against the line. The line's
  test is whether the rule changes the form every rule takes, who may review
  or approve, or whether the process applies (reaching), or what the process
  asks at one step under a decision already recorded (not reaching). All
  seven are consistent with the line; no gap is accepted:
  - EM-008 — §3 blocks on a reserved question as on ambiguity. What the
    blocking step asks; under §3 as adopted by ADR-0001. Consistent.
  - EM-009 — a repair names its class and siblings. What a repair carries;
    under §6 and the falsification gate. Consistent.
  - EM-010 — a review answers two questions in two columns. What the review
    step asks of a change; under ADR-0002, which decided who reviews and what
    the reviewer receives. Consistent, and the nearest of the seven to the
    line: it changed the form of every critical-tier review, but not who
    reviews, what a rule is, or whether the process applies. A reader who
    thinks it crossed the line has a finding against the line, not the
    practice, and the falsifier says what that finding would need.
  - EM-011 — review runs in the reviewer's own worktree; the tree is checked
    afterwards. Where the review runs; under ADR-0002. Consistent, and the
    document's own example.
  - EM-012 — trivial changes may share a batch ticket. A path through the
    lifecycle ADR-0001 adopted. Consistent.
  - EM-016 — the policy's map and the model's index, kept true in the same
    commit. How the documents are navigated, not what a rule is; under
    ADR-0001. Consistent.
  - EM-019-001 — a measured figure is read from a command the description
    names. What a description carries; under §6. Consistent.
- [x] AC3: the line carries its own **Retired when:**, distinct from the one
  the trigger list already has. The "When to write one" section holds 1
  line beginning `**Retired when:**` at the baseline ce59c8f and 2 at
  f51ad72, from `git show <commit>:docs/adr-process.md | sed -n '/^## When
  to write one/,/^## Structure/p' | grep -c '^\*\*Retired when:\*\*'` run
  at f51ad72 for each commit. The trigger list's names a regression with the
  record present or a set of records nobody reads; the line's names a rule
  recorded in no decision record that a later contributor undid or
  contradicted for want of one.
- [ ] AC4: an independent agent reviews this and records findings in two
  columns — round 1 pending; see Review.

### Falsification
N/A — a documentation change with no suite. Per acceptance criterion, what a
reader does differently:
- AC1 — a contributor working a rule-adding ticket reads the trigger, reaches
  the line, and writes no decision record for a rule added under an existing
  decision, where before the trigger's words told them to and the practice
  told them not to and nothing said which was right. A contributor whose
  ticket changes how the process is governed — the form of every rule, who
  reviews, whether the process applies — writes one, as ADR-0003 did.
- AC2 — a reader auditing the seven tickets against the trigger finds the
  practice stated as the line rather than a lapse against it, and does not
  raise a ticket to write seven records retrospectively.
- AC3 — a reviewer who finds a rule added under an existing decision undone
  by a contributor who could not see why it was there has a falsifier to
  match the finding to, and the second such finding retires the line rather
  than being argued case by case. A reviewer whose finding is that the
  trigger list produces records nobody reads matches the trigger list's own
  falsifier, which is unchanged.
- AC4 — pending.

### Out of scope (per ticket)
- No decision record was written for any of the seven. Under the line none
  was owed; had the answer gone the other way it would have been a separate
  ticket, as the ticket's Out of scope says.
- No other trigger in the list was touched, and the test sentence ("if the
  decision affects multiple tickets or constrains future work") is unchanged;
  the new paragraph says how it reads under the line rather than rewriting
  it.
- `templates/ADR.md` restates the trigger as "A workflow rule in
  CONTRIBUTING.md changes" and was not touched: the template is outside the
  ticket's Files, and EM-018 owns the templates' references to files this
  repository does not publish.
- The rule-adding tickets outside the seven the ticket names — EM-006,
  EM-007, EM-012-001, EM-014-001, EM-020 and EM-021 — were not assessed under
  AC2, which names its population. Each adds a rule inside an existing
  document under an existing decision and reads the same way; none is claimed
  here as checked.

### How to verify
1. `git diff ce59c8f..f51ad72 -- docs/adr-process.md` — one paragraph and
   one **Retired when:** added to "When to write one"; nothing removed.
2. Read the whole "When to write one" section at f51ad72 and check that the
   two examples sit on opposite sides of the line as stated, and that the
   trigger list's own **Retired when:** is unchanged.
3. `git diff ce59c8f..f51ad72 --stat -- docs/ai-contributor-policy.md` —
   empty; the map row for `docs/adr-process.md` still settles "Is this
   decision a record, and what does that record carry?" and no section was
   added, removed or renamed, so the same-commit rule asked for no map change.
4. For AC2, open each of the seven tickets in `docs/tickets/done/` and read
   its Behaviour against the line's test as restated under AC2.

### Risks / follow-ups
- **Cost of the addition.** `docs/adr-process.md` grows from 563 words at
  ce59c8f to 950 at f51ad72, from `git show ce59c8f:docs/adr-process.md |
  wc -w` and `wc -w < docs/adr-process.md` run at f51ad72; the diff is 33
  insertions and 0 deletions from `git diff --stat ce59c8f..f51ad72 --
  docs/adr-process.md`. That is the brief EM-016 set out to bound growing by
  one paragraph, paid by every reader of this document, so that a reader
  with a rule-adding ticket has an answer instead of a contradiction.
- **The test sentence still reads wider than the line.** "Constrains future
  work" catches a rule added under an existing decision on a literal
  reading; the new paragraph states how the test reads under the line. A
  reviewer may find that the test should be reworded rather than glossed;
  that is a change to the test, which the ticket's Out of scope reserves
  from this change ("any other trigger in the list"), and would be a child
  ticket.
- **The line rests on the ticket being the record.** It holds only while
  rule-adding tickets carry what a record would — instances in Context, rule
  and falsifier in Behaviour, review in the description. EM-021's bar and
  ADR-0003's obligation make the first two required for new tickets; a
  project adopting these documents without both should expect the line's
  falsifier to be met sooner.
- No child ticket raised.

### Review
Critical tier. One row per independent review round; the total is derived
from the rows and never asserted beside them.

| Round | Must-fix | Where (rules / lists / documents / tests) | Inside previous round's fix | Repaired by |
|---|---|---|---|---|
| 1 | — | — | — | — |

Round 1 pending.
