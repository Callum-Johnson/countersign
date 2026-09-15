---
id: EM-019-001-001-001
title: The decision-record test reads wider than the line drawn beneath it
status: done
tier: critical
complexity: S
dependencies: [EM-019-001-001]
claimed_by: claude-opus-5
claimed_at: 2026-09-15
closed_at: 2026-09-15
---

# EM-019-001-001-001 — The decision-record test reads wider than the line

## Context

Raised by the independent review of EM-019-001-001 (finding R1.4 of round
1).

`docs/adr-process.md`, "When to write one", states a test: "if the decision
affects multiple tickets or constrains future work, it is an ADR. If it
affects only the ticket in hand, the ticket is enough." EM-019-001-001 draws
a line beneath it under which a rule added inside a document under an
existing decision owes no record, and says how the test reads under the
line: the constraint such a rule places on future work is the existing
decision's. On a literal reading the test still reaches every such rule —
each constrains future work — so the section carries a test and a gloss on
the test, and a reader who stops at the test gets the wider answer.

EM-019-001-001's Out of scope reserves the test and every other trigger, so
the gloss is what that ticket could do. Rewording the test is this one.

## Specification

Documentation change only.

### Files

- `docs/adr-process.md` — "When to write one", the test sentence and the
  gloss on it in the paragraph beginning **What "a workflow rule changes"
  reaches**.

### Public surface

N/A — this repository publishes documents. One sentence is made to agree
with the line beneath it.

### Behaviour

- The test sentence, read on its own, gives the same answer the line gives:
  a decision that changes how the process is governed, or constrains work
  beyond the ticket in hand and sits under no decision already recorded, is
  a record; a rule added under a recorded decision is not, whatever it
  constrains.
- The gloss — "The test above reads the same way" and the clause that
  follows it — is removed, since a test that says what it means needs no
  gloss.
- This ticket amends a sentence and adds no rule, so it states no new
  falsifier: the test retires with the trigger list's existing **Retired
  when:**, and the line with its own. The second-instance bar in
  `docs/tier-review-model.md`, "Retiring a control", governs a rule's entry
  as a ticket's own subject and does not reach this amendment.

## Acceptance criteria

1. AC1: the test sentence, read without the paragraph beneath it, places
   EM-011's review-isolation rule on the no-record side and ADR-0003 on the
   record side.
2. AC2: the gloss on the test is gone from the line's paragraph, and the
   line's examples and falsifier are unchanged.
3. AC3: An independent agent reviews this and records findings in two
   columns.

## Out of scope

- The line itself, its examples and its falsifier.
- Any other trigger in the list, and the section's existing **Retired
  when:**.
- `templates/ADR.md`, which restates the trigger; EM-018 owns the
  templates.

## References

- `docs/adr-process.md`, "When to write one".
- EM-019-001-001 — the line, and the review finding this ticket records.
- ADR-0003 and EM-011 — the two examples the test must agree with.

## Notes

Proposed `critical`: `docs/adr-process.md` is a process document, which
ADR-0002 classifies as process-surface, and an author may raise but never
lower. EM-007-002 owns whether that classification is right.

## PR Description

### Ticket
EM-019-001-001-001 — The decision-record test reads wider than the line drawn
beneath it.

### Tier
`standard`, on one independent review pass. The ticket's Notes proposed
`critical` on ADR-0002's process-surface classification and named EM-007-002
as owning whether that was right. EM-007-002 has since closed and ADR-0004
decides it: a change to a process document is `standard` and its review is one
independent pass, closing on that pass. `docs/adr-process.md` is a process
document. The frontmatter still reads `critical` and is left as it stands,
because lowering a tier is not the executor's to do; the pass ran against
3a430c9 and is row 1 of the Review table.

### Summary
The test read "if the decision affects multiple tickets or constrains future
work, it is an ADR", which on a literal reading reached every rule added under
an existing decision, since each constrains future work. The line beneath it
says such a rule owes no record, and a gloss reconciled the two. The test now
states the line in its own terms and the gloss is gone.

### Acceptance criteria
- [x] AC1: the test sentence, read without the paragraph beneath it, places
  EM-011's review-isolation rule on the no-record side and ADR-0003 on the
  record side. Worked through the sentence as it now stands:
  - **EM-011's review-isolation rule** (`docs/quality-gates.md`, "Review
    isolation"). First disjunct: does it change how the process itself is
    governed? No — it says where a review runs, which is a step inside the
    process. Second disjunct: it constrains work beyond the ticket in hand,
    but it does not sit under *no* existing decision, because ADR-0002 decided
    the review it places; the disjunct does not fire. The next sentence then
    settles it: the rule does no more than apply ADR-0002 at one step, and it
    is not being retired or amended. **No record owed.**
  - **ADR-0003.** First disjunct fires: the falsifier obligation changed the
    form every rule in `docs/` takes and how the rule set can shrink, which is
    the governance level rather than a step. The next sentence does not reach
    it — it is a decision, not a rule applying one, and ADR-0001 decided that
    this repository is governed by its documented process, not that a rule is
    held to evidence. **Record owed.**
- [x] AC2: the gloss is gone from the line's paragraph, and the line's
  examples and falsifier are unchanged. The reviewer confirmed the three
  examples byte-identical — ADR-0003, EM-011 and EM-021 — with only the gloss
  removed between the EM-021 sentence and "This is the practice", and both
  **Retired when:** lines untouched.
- [x] AC3: an independent agent reviewed this and recorded findings in two
  columns. It ran against 3a430c9, having received the ticket, the documents
  and the two questions but not the executor's reasoning, and returned three
  must-fixes over four findings — one of them in the second column, which is
  the column this repository added because a review briefed to look hard
  looks only at the first. Row 1 of the Review table; repairs at 6a0118d.

### Falsification
N/A for a behavioural claim — this repository publishes documents and runs no
suite. Per criterion, what a reader does differently: a contributor asking
whether a rule they are adding owes a decision record gets the same answer
from the test as from the paragraph beneath it, instead of a wider one if they
stop at the test.

For each must-fix repaired, per the contributor policy's §6:

- R1.2 — class: **which words did the rewrite substitute for the line's own,
  and does the substitute reach the same set?** "a decision already recorded"
  for the line's "an existing decision" is the instance. The question was
  asked of every term the new test carries that the line also uses. Siblings:
  - **"recorded"** — the instance, and the substitution that narrows. The line
    exempts a rule added "under an existing decision"; the test exempted one
    added under a decision *already recorded*, which is a smaller set. Checked
    against the seven rules the same paragraph names as having owed no record:
    EM-008's clause in §3, EM-012's batching rule, EM-016's bound brief and
    EM-019-001's figures rule sit under no record in `docs/adr/`, so the test
    demanded a record for each where the line refuses one. Repaired by
    carrying the line's term.
  - **"added under"** — checked, and it was the second half of the same
    defect: an amendment to an existing rule is not a rule "added", so the
    sentence missed amendments entirely. Repaired in the same clause: the
    sentence now reaches a rule that "does no more than apply an existing
    decision at one step", which covers adding and extending alike.
  - **"constrains future work" → "constrains work beyond the ticket in hand"**
    — checked and sound. It narrows nothing the line relies on; it is the
    original test's own second limb, made explicit.
  What a reader does differently: an executor extending EM-012's batching rule
  reads the test alone, finds the rule applies an existing decision at one
  step, and writes no record — which is what the paragraph four lines below
  has always said and what the practice has been.
- R1.1 — class: **which cases does an absolute exclusion swallow that the
  document elsewhere puts on the record side?** The retired-or-amended case is
  the instance. The question was asked of every other statement in the section
  that assigns a case to the record side. Siblings:
  - **The trigger bullet "A workflow rule changes — including a rule retired
    or amended under `docs/tier-review-model.md`, 'Retiring a control'"** —
    the instance. A rule can both sit under a recorded decision and be retired
    under a matched falsifier; the exclusion, read alone, put it on the
    no-record side, and its text would leave the document with the finding
    that matched surviving nowhere. Repaired by a carve-out naming that
    section, with the reason stated: there the record *is* the control.
  - **"Retiring a control", Amendment with record** — checked; it says the
    same thing for an amendment in place, and the carve-out names retirement
    and amendment together, so both are covered by one clause.
  - **The other four triggers** — a dependency added or swapped, a public API
    shape change, a locked design decision revised, a new top-level package —
    checked, and none can be a rule added under an existing decision, so the
    exclusion cannot reach them.
  What a reader does differently: a retirement ticket writes its record, and
  the retired text and the finding that matched it survive in the one place
  they can, rather than being exempted because the rule happened to sit under
  a decision that had one.
- R1.3 — note. Repaired in the round; a note carries nothing under §6 as
  EM-009-001 narrowed it.

### Out of scope (per ticket)
Confirmed; nothing here exceeds it.
- The line itself, its examples and its falsifier — untouched.
- Any other trigger, and the section's existing **Retired when:** — untouched.
- `templates/ADR.md`, which EM-018 owns — untouched. The review found it still
  carries the superseded test; see the routed finding below.

### Routed, not repaired
R1.4 is a must-fix the reviewer recorded and this ticket does not repair.
`templates/ADR.md` line 94 restates the test in its old words — "if the
decision affects multiple tickets or constrains future work, ADR it" — so the
wider reading removed here is still available one file away. The ticket's Out
of scope reserves the templates to EM-018, which has closed, so the finding
goes to a ticket raised to own it under the second condition of "When review
ends": **EM-018-002**. That one must-fix is discharged by raising it.

### How to verify
1. `sed -n '/^The test: a decision is an ADR/,/ticket is enough\./p' docs/adr-process.md`
   — the test as it now stands. Cover the paragraph beneath it and work
   EM-011's review-isolation rule and ADR-0003 through the sentence; the two
   answers differ, which is AC1.
2. `git diff main...HEAD -- docs/adr-process.md` — two hunks, the test sentence
   and the removed gloss, and nothing in the line's examples or either
   **Retired when:** line.
3. `grep -n 'affects multiple tickets' templates/ADR.md` — one hit, which is
   the routed finding EM-018-002 owns, and no hit in `docs/`.
4. `grep -c 'Retiring a control' docs/adr-process.md` — the carve-out names
   the section the trigger bullet already named, so the two agree.

### Risks / follow-ups
- **What this settles for EM-020-001.** That ticket's blocker records a
  disagreement between the trigger bullet and the line, on whether a clause
  loosening the contributor policy's §3 — which governs when to block, and is
  amended under "Retiring a control" — owes a decision record. It names this
  ticket as the one that owns the disagreement. Worked through the test as it
  now stands: the clause amends a rule under "Retiring a control", so the
  carve-out fires and **a record is owed**, agreeing with the trigger bullet.
  Before R1.1's repair the answer turned on whether §3's parent decision
  happened to be written into `docs/adr/`, which is a fact neither the trigger
  nor the line turns on. The maintainer holds EM-020-001 and this is stated
  for them, not decided for them: it is what the document now says, and they
  may still reach a different answer and amend it.
- The test is one sentence longer than it was and carries a named exception.
  A test that needs an exception is worth watching: if a second exception is
  ever needed, that is the second instance "A rule needs a second instance"
  asks for, and the shape to consider then is moving the test's content into
  the line and leaving one statement rather than two.

### Review
One independent review pass, per "The operative test" for a change to a
process document. No second pass is taken.

| Round | Must-fix | Where (rules / lists / documents / tests) | Inside previous round's fix | Repaired by |
|---|---|---|---|---|
| 1 | 3 (of 4 findings) | documents: the test narrowed the line's "an existing decision" to one already recorded, so it demanded a record for rules sitting under unrecorded decisions — four of the seven the same paragraph names — and for this change itself (must-fix, second column); the exclusion was absolute and swallowed a rule retired or amended under "Retiring a control", where the record is the control and the trigger bullet above puts it on the record side (must-fix); `templates/ADR.md` still restates the test in its superseded form, which the ticket's Out of scope reserves to EM-018 (must-fix, routed to EM-018-002); nothing ordered the test's two sentences, so a rule that is both returns two answers | — | 6a0118d |

Derived from the row and not asserted beside it: three must-fixes over one
review round, of which two are repaired here and one is discharged by raising
EM-018-002. Round 1 has no round before it, so its inside-previous-fix cell
reads `—` and no line is uncountable.

- R1.2 · refuses · must-fix · `docs/adr-process.md`, the test's "sits under no decision already recorded" against the line's "under an existing decision" · the test narrows the line to decisions written into `docs/adr/`, and four of the seven rules the same paragraph names as owing no record sit under decisions that were never recorded, so an executor reading the test alone writes a record the paragraph below refuses; the decision-record process itself sits under no record, so the test applied to this change demanded one — remedy: carry the line's term and leave "recorded" out; cost, if the remedy tightens a control: none — the remedy removes a refusal; inside previous fix: —
- R1.1 · permits · must-fix · `docs/adr-process.md`, the test's exclusion against the trigger bullet and "Retiring a control", **Amendment with record** · the exclusion carries no carve-out for a rule retired or amended under that section, so a rule sitting under a recorded decision and later retired under a matched falsifier lands on the no-record side, and its text leaves the document with the matching finding surviving nowhere — remedy: carve out retirement and amendment, where the record is the control; cost, if the remedy tightens a control: retirement and amendment tickets pay it, and each already owed its record under the trigger bullet and under Amendment with record, so no change owes a record it did not already owe; inside previous fix: —
- R1.4 · permits · must-fix · `templates/ADR.md`, "When to write an ADR vs not", closing sentence · the template restates the test verbatim in its superseded form, so the wider reading this ticket removes is still available one file away and the repository states one test two ways that disagree — remedy: the ticket that owns the templates replaces it or points at the document; routed to EM-018-002 under the second condition of "When review ends", since Out of scope reserves `templates/ADR.md`; cost, if the remedy tightens a control: none — a restatement, not a control; inside previous fix: —
- R1.3 · permits · note · `docs/adr-process.md`, the test's two sentences · no order is stated between them, so a rule that both changes how the process is governed and sits under an existing decision returns two answers — remedy: scope the second sentence to a rule that does no more than apply an existing decision at one step; cost: none, it names a priority the test already assumed; inside previous fix: —

The reviewer found a finding in the second column and it is the one that
mattered most: R1.2 is an over-tightening, a test demanding records the
document elsewhere refuses. It is recorded in that column, and it is a
must-fix of the same rank as a first-column finding, which is what "What a
review reports" requires.

### Definition of Done (all tiers)
The four machine checks do not apply to a repository that publishes documents
and runs no suite; the falsification gate is discharged above, with N/A for
the behavioural claim and a class line per must-fix repaired. Every measured
figure names its baseline in the same sentence and is read from the command
named beside it. The independent pass a process-document change takes has run
and is recorded.
