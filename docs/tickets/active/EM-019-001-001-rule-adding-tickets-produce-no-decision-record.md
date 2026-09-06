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
on the second, EM-021's second-instance bar is placed on the second side with
its reason, the document says this is the practice the repository has
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
  one", landed at f51ad72 and as it stands at 8fe386c. ADR-0003 is named on
  the reaching side, with why no document could have carried it as one rule
  among the others; EM-011's rule, `docs/quality-gates.md`, "Review
  isolation", is named on the other, with the decision it sits under
  (ADR-0002); EM-021, routed here by EM-021's own review, is named on the
  second side with its reason.
- [x] AC2: each of the seven tickets checked against the line. The line's
  test is whether the rule changes the form every rule takes, who may review
  or approve, or whether the process applies to the repository (reaching), or
  what the process asks at one step under a decision already recorded (not
  reaching) — in one question, whether the change acts on the rules as a set
  or on one rule added or extended in place. All seven are consistent with
  the line; no gap is accepted:
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
    lifecycle ADR-0001 adopted; the process still applies to the repository,
    and to the change, which takes a ticket. Consistent.
  - EM-016 — the policy's map and the model's index, kept true in the same
    commit. How the documents are navigated, not what a rule is; under
    ADR-0001. Consistent.
  - EM-019-001 — a measured figure is read from a command the description
    names. What a description carries; under §6. Consistent.
- [x] AC3: the line carries its own **Retired when:**, distinct from the one
  the trigger list already has. The "When to write one" section holds 1
  line beginning `**Retired when:**` at the baseline ce59c8f and 2 at
  8fe386c, from `git show <commit>:docs/adr-process.md | sed -n '/^## When
  to write one/,/^## Structure/p' | grep -c '^\*\*Retired when:\*\*'` run
  at 8fe386c for each commit. The trigger list's names a regression with the
  record present or a set of records nobody reads; the line's names a rule
  recorded in no decision record that a later contributor undid or
  contradicted for want of one.
- [ ] AC4: an independent agent reviews this and records findings in two
  columns — round 1 recorded below; round 2 pending.

### Falsification
N/A — a documentation change with no suite. Per acceptance criterion, what a
reader does differently:
- AC1 — a contributor working a rule-adding ticket reads the trigger, reaches
  the line, and writes no decision record for a rule added under an existing
  decision, where before the trigger's words told them to and the practice
  told them not to and nothing said which was right. A contributor whose
  ticket changes how the process is governed — the form of every rule, who
  reviews, whether the process applies to the repository — writes one, as
  ADR-0003 did.
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

For each review finding repaired (contributor policy §6); the change has no
suite, so each sibling says what a reader does differently:
- R1.1 — class: which routed or live rule-adding cases does the line leave
  undecidable? The question enumerates the rule-adding tickets closed on
  this repository outside the seven the ticket names, read from
  `docs/tickets/done/` at 8fe386c: EM-021 (the routed case) and its
  siblings EM-006, EM-007, EM-012-001, EM-014-001 and EM-020. Each was
  checked against the line as repaired, and each falls on the second side:
  - EM-021 — the second-instance bar; one paragraph added under ADR-0003's
    decision, no rule rewritten. Named in the document. A contributor whose
    ticket sets what a rule-adding ticket must carry reads EM-021 on the
    second side and writes no record.
  - EM-006 — the falsification gate; adds a gate to `docs/quality-gates.md`
    and acts on tests, not on the rules. The nearest sibling, since
    ADR-0003 calls itself EM-006's generalisation: what separates them is
    that ADR-0003's migration rewrote every rule in `docs/` and EM-006
    rewrote none. A contributor adding a gate reads it on the second side.
  - EM-007 — "When review ends"; a section added under ADR-0002. A
    contributor adding a stopping rule to the review reads it on the
    second side.
  - EM-012-001 — the trivial/standard clause; one sentence extended in place
    in the operative test, with no record. This sibling is what the read
    of the whole section caught after the repair: the one-question form
    as first written ("act on the rules already there, or add one")
    placed it on the record side, and 8fe386c reworded the question to
    "on the rules as a set, or on one rule added or extended in place". A
    contributor extending one rule's sentence outside "Retiring a control"
    reads it on the second side.
  - EM-014-001 — the class signal; a paragraph added under ADR-0002 and
    ADR-0003. Second side.
  - EM-020 — read the whole section before handing a repair back; a
    paragraph added under ADR-0002. Second side.
- R1.2 — repair of the instance.
- R1.5 — repair of the instance.

### Out of scope (per ticket)
- No decision record was written for any of the seven, or for EM-021.
  Under the line none was owed; had the answer gone the other way it would
  have been a separate ticket, as the ticket's Out of scope says.
- No other trigger in the list was touched, and the test sentence ("if the
  decision affects multiple tickets or constrains future work") is unchanged;
  the new paragraph says how it reads under the line rather than rewriting
  it. Rewording it is EM-019-001-001-001, raised in the round from R1.4.
- `templates/ADR.md` restates the trigger as "A workflow rule in
  CONTRIBUTING.md changes" and was not touched: the template is outside the
  ticket's Files, and EM-018 owns the templates' references to files this
  repository does not publish.
- "Decisions about the process are themselves ADRs", later in the same
  document, was not touched: outside the ticket's Files. R1.3 under Risks
  carries the sentence a later change would add.
- The rule-adding tickets outside the seven the ticket names were checked in
  the round-1 repair as R1.1's siblings, above, not under AC2, which names
  its population.

### How to verify
1. `git diff ce59c8f..8fe386c -- docs/adr-process.md` — one paragraph and
   one **Retired when:** added to "When to write one"; nothing removed.
2. Read the whole "When to write one" section at 8fe386c and check that the
   three named cases sit on the sides stated, that the one-question form
   agrees with the clauses before it, and that the trigger list's own
   **Retired when:** is unchanged.
3. `git diff ce59c8f..8fe386c --stat -- docs/ai-contributor-policy.md` —
   empty; the map row for `docs/adr-process.md` still settles "Is this
   decision a record, and what does that record carry?" and no section was
   added, removed or renamed, so the same-commit rule asked for no map change.
4. For AC2, open each of the seven tickets in `docs/tickets/done/` and read
   its Behaviour against the line's test as restated under AC2; for R1.1's
   siblings, the six named there.
5. `ls docs/tickets/ready/EM-019-001-001-001-*` and the board row — the
   child ticket from R1.4.

### Risks / follow-ups
- **Cost of the addition.** `docs/adr-process.md` grows from 563 words at
  ce59c8f to 1056 at 8fe386c, from `git show ce59c8f:docs/adr-process.md |
  wc -w` and `wc -w < docs/adr-process.md` run at 8fe386c; the diff is 42
  insertions and 0 deletions from `git diff --stat ce59c8f..8fe386c --
  docs/adr-process.md`. That is the brief EM-016 set out to bound growing by
  one paragraph, paid by every reader of this document, so that a reader
  with a rule-adding ticket has an answer instead of a contradiction. The
  round-1 repair added a third named case and the one-question form to the
  same paragraph.
- **R1.3 — a second answer in the same document.** "Decisions about the
  process are themselves ADRs" still reads "Recording process changes the
  same way as technical ones is what keeps it honest" with no reference to
  the line. Outside this ticket's Files, so not edited here. The sentence a
  later change would add after it: "Which process changes are decisions, and
  which are rules added under one, is drawn in 'When to write one'." One
  sentence; no rule.
- **R1.4 — the test sentence still reads wider than the line.** "Constrains
  future work" catches a rule added under an existing decision on a literal
  reading; the new paragraph states how the test reads under the line. This
  is work, and is raised as **EM-019-001-001-001**, `ready/`, critical,
  dependent on this ticket: the test reworded to agree with the line and the
  gloss removed. It is a child ticket rather than a Risks note because it
  changes a sentence in a rule-bearing document, which the parent's Out of
  scope reserves.
- **The line rests on the ticket being the record.** It holds only while
  rule-adding tickets carry what a record would — instances in Context, rule
  and falsifier in the ticket file, review in the description. EM-021's bar
  and ADR-0003's obligation make the first two required for new tickets; a
  project adopting these documents without both should expect the line's
  falsifier to be met sooner.
- **The wrapping** of the repaired paragraph is uneven where lines were
  re-flowed; the tier review model's wrapping clause says that is not a
  finding.

### Review
Critical tier. One row per independent review round; the total is derived
from the rows and never asserted beside them.

| Round | Must-fix | Where (rules / lists / documents / tests) | Inside previous round's fix | Repaired by |
|---|---|---|---|---|
| 1 | 1 | documents | — | a2ebce6, and 8fe386c from the whole-section read |
| 2 | — | — | — | — |

Post-review check after round 1, run at 4278ca5 before the repair:
`git status --porcelain` empty; `git worktree list` shows the reviewer's
`A:/projects/wt/review-EM-019-001-001` at 4278ca5, detached, as the brief
said to expect, still registered at the time of the check, and sibling
ticket worktrees under `A:/projects/wt/` belonging to other tickets; nothing
inside the tree under review. No finding against the review.

Round 1, of 4278ca5:
- R1.1 · permits · "What 'a workflow rule changes' reaches", the example
  pair · EM-021, routed to this ticket by EM-021's own round-1 review as the
  ticket that owns the question, was undecidable under the line: it changed
  what every rule-adding ticket carries and what a rule needs to enter, the
  same kind of act as ADR-0003 on the reaching side, and the model's index
  pairs how a rule leaves with what one needs before it enters — remedy:
  one sentence placing EM-021 on a side with its reason; cost: one sentence,
  and a record only if the first side. Must-fix. Placed on the second side
  at a2ebce6: EM-021 added one paragraph under ADR-0003's decision and
  rewrote no rule, where ADR-0003's migration added a line to every rule.
  Class and siblings under Falsification; inside previous fix: no (first
  round).
- R1.2 · permits · "whether the process applies at all" · literally reached
  by EM-012, which AC2 places on the second side — remedy: "whether the
  process applies to the repository at all"; cost: none. Note; repaired at
  a2ebce6. Inside previous fix: no.
- R1.3 · permits · "Decisions about the process are themselves ADRs" · still
  gives a second answer in the same document with no reference to the line
  — remedy: one cross-reference sentence; cost: one sentence. Note; outside
  Files, recorded under Risks / follow-ups with the sentence. Inside
  previous fix: no.
- R1.4 · permits · the test sentence · "constrains future work" still
  literally reaches every rule; the gloss follows it — remedy: a child
  ticket; cost: a ticket. Note; raised as EM-019-001-001-001 at a2ebce6.
  Inside previous fix: no.
- R1.5 · permits · "the Behaviour states the rule and its falsifier" ·
  EM-008, EM-009, EM-011 and EM-012 were ADR-0003-exempt and stated theirs
  in the description, not the Behaviour — remedy: "the ticket file states";
  cost: none. Note; repaired at a2ebce6. Inside previous fix: no.
- R1.6 · refuses · none · the line removes an obligation and forbids
  nothing; it errs narrow by design and its falsifier names that direction.
  No second-column must-fix.

Round 2 pending.
