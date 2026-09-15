---
id: EM-007-002-001
title: The operative test's one-line summary omits the process-surface clause
status: done
tier: standard
complexity: S
dependencies: [EM-007-002]
claimed_by: claude-opus-5
claimed_at: 2026-09-15
closed_at: 2026-09-15
---

# EM-007-002-001 — The one-line summary omits the process-surface clause

## Context

Raised while working EM-007-002, under the contributor policy's §4.

`docs/tier-review-model.md`, "The operative test", closes with a summary
introduced by "In one line":

> **Could an existing caller, or a seeded run, notice this change without
> opting in? If yes, `critical`. If no, `standard` — or `trivial`, where
> nothing a program executes or a caller reads as a contract is touched.**

Its `critical` limb carries clauses 1 to 4 and not clause 5. A schema
migration, a CI configuration change and a change to the review model are
`critical` by clause 5, and no existing caller or seeded run notices any of
them, so the summary sends all three to `standard` or `trivial`.

This is visible on this repository rather than hypothetical. EM-007-002
writes into the same section the line that decides when a change to a
process document is `critical` — when it adds, alters or retires a rule or
a procedure — and that line hangs off clause 5. A contributor who runs the
summary instead of the clauses gets `trivial` for a rule change, which is
the answer the section now spends a page refusing.

The summary was already repaired once, by EM-012-001: round 1, finding
R1.3, a second-column finding its Review section records as "the one-line
summary refusing trivial to every documentation change". The remedy added
the `trivial` outcome. The `critical` limb was not in that finding's scope.

## Specification

Documentation change only.

### Files

- `docs/tier-review-model.md` — "The operative test", the block quote
  introduced by "In one line".

### Public surface

N/A — this repository publishes documents. One summary is made to agree
with the clauses it summarises.

### Behaviour

- The summary's `critical` limb returns `critical` for a change any of the
  five clauses catches, clause 5 included, so that a contributor who reads
  only the summary gets the same tier as one who runs the clauses.
- The five clauses are unchanged; this ticket edits the summary of them.
- No new rule is added, so no new falsifier is stated: the summary retires
  with the **Retired when:** line already beneath it.

## Acceptance criteria

1. AC1: the summary, read without the clauses above it, returns `critical`
   for a CI configuration change and for a change that adds a rule to a
   process document.
2. AC2: the summary still returns the same tier as the clauses for the
   changes it already answered correctly, and stays one sentence a
   contributor can hold.
3. AC3: the five clauses, the `trivial` line, and the process-document
   paragraph are unchanged.
4. AC4: an independent agent reviews this and records findings in two
   columns.

## Out of scope

- The five clauses.
- The `trivial` line and the process-document paragraph beneath it.
- What any tier requires.

## References

- `docs/tier-review-model.md`, "The operative test".
- EM-012-001 — the ticket that last repaired this summary, and its round-1
  record.
- EM-007-002 — the ticket this was raised under, which adds the paragraph
  that makes the omission load-bearing.

## Notes

Proposed `critical` when raised, under the paragraph EM-007-002 then added
to this same section.

**Read against the maintainer's answer to EM-007-002, 2026-09-10.** A change
to a process document is now `standard` on one independent pass, neither
`trivial` nor `critical`, and the tier is not raised; the frontmatter says
`standard` for that reason. What the answer moots: the Context's second and
third paragraphs, which motivate this ticket from the `critical`/`trivial`
line, which never landed; and the second half of AC1, since the summary's
process-document limb is written by EM-007-002 — "A process document is
`standard`, on one pass, whatever the answer." What stands, and is this
ticket: the summary's `critical` limb carries clauses 1 to 4 and not clause
5, so a contributor reading only the summary gets `standard` for a CI
configuration change and a schema migration, which clause 5 makes
`critical`. AC1 is read as its first half; AC3's "process-document
paragraph" is the one EM-007-002 lands; AC4 is the one pass.

## PR Description

### Ticket
EM-007-002-001 — The operative test's one-line summary omits the
process-surface clause.

### Tier
`standard`, on one independent review pass. A change to
`docs/tier-review-model.md` is a change to a process document, which "The
operative test" fixes at that tier. The frontmatter reads `standard` for the
reason the ticket's Notes give. The pass ran against 0c0ec7e and is row 1 of
the Review table.

### Summary
The summary's `critical` limb asked only whether an existing caller or a
seeded run would notice, which is clauses 1 to 4. A schema migration and a CI
configuration change are `critical` by clause 5 and noticed by neither, so a
contributor reading only the summary got `standard` or `trivial` for both. The
limb now asks clause 5's question too, and the closing sentence carries the
carve-out for a change that is both a process document and something a program
executes.

### Acceptance criteria
- [x] AC1, **read as its first half**, which is the ticket's own recorded
  scope and not an executor judgement: the ticket's Notes say "AC1 is read as
  its first half", and ADR-0004's Migration amends the ticket in terms —
  EM-007-002-001 "stands for a CI configuration change and a schema migration
  and is amended here for a process document". So the criterion is that the
  summary returns `critical` for a CI configuration change. Worked through the
  summary alone: no caller and no seeded run notices an edit to a CI workflow's
  job steps, the second disjunct holds, a disjunctive question with one true
  disjunct is answered yes, and "If yes, `critical`" fires. The `trivial`
  branch sits inside `If no` and does not reach it, and the closing sentence
  fires only for a process document. Returns `critical`.

  AC1's second half — that the summary return `critical` for a change that
  adds a rule to a process document — is overtaken and is **not** implemented.
  Clause 5 no longer reaches process documents at all: EM-007-002-003 amended
  it on 2026-09-15 so that a change to the review model is sent to the
  paragraph below, and a schema migration and a CI configuration change are
  what remain. ADR-0004 decides such a change is `standard` on one pass, and
  its Alternative 2 records the `critical`-per-rule-change reading as rejected
  after four passes. A summary returning `critical` there would contradict the
  decision in force and summarise no clause.
- [x] AC2: the summary returns the same tier as the clauses for the changes it
  already answered correctly, and stays one sentence a contributor can hold.
  Worked through:
  - **Contract change** (clause 1): an existing caller could observe the
    difference → first disjunct yes → `critical`. Clauses: `critical`. Agree.
  - **Pure documentation** — a case study, prose stating no rules: both
    disjuncts no → `If no` → nothing a program executes or a caller reads as a
    contract is touched → `trivial`. Clauses: `trivial` by the same wording.
    Agree.
  - **Process-document change, rule-adding** — a rule added to
    `docs/quality-gates.md`: both disjuncts no, closing sentence fires, the
    change touches nothing a program executes → `standard`, one pass. Clauses:
    no clause holds, the process-document paragraph → `standard`, one pass.
    Agree.
  - **The hybrid** — a process document that is also something a program
    executes: first sentence yes, closing sentence's carve-out fires, so the
    answer above stands → `critical`. Clauses: classed on the other thing →
    `critical`. Agree. This case is what R1.1 repaired; before the repair the
    summary returned `standard` here and the clauses returned `critical`.
  Holdability: four short sentences, as before; the first is now 24 words.
- [x] AC3: the five clauses, the `trivial` line and the process-document
  paragraph are unchanged. `git diff main...HEAD -- docs/tier-review-model.md`,
  run after 39e89dd, is one hunk entirely inside the block quote under "In one
  line".
- [x] AC4: one independent review pass, run against 0c0ec7e by an agent that
  did not perform the work and did not receive the executor's reasoning,
  recorded as row 1 of the Review table below. It returned one must-fix over
  two findings, repaired at 39e89dd.

### Falsification
N/A for a behavioural claim — this repository publishes documents and runs no
suite. Per criterion, what a reader does differently: a contributor who reads
only the summary and is editing a CI workflow or a schema migration now gets
`critical`, which is what running the clauses gives them, instead of
`standard` or `trivial`.

For the review finding repaired, per the contributor policy's §6:

- R1.1 — class: **which sentences of the summary override an answer an earlier
  sentence gives, and do their overrides match the clauses?** The closing
  sentence's "whatever the answer" is the instance. The question was asked of
  every sentence in the block quote. Siblings, each checked:
  - **"A process document is `standard`, on one pass, whatever the answer"** —
    the instance. It overrode the limb this ticket added, so a change that is
    both a process document and something a program executes returned
    `standard` where the clauses return `critical`. The paragraph beneath the
    test says such a change "is classed by the rest of this test on that other
    thing; this paragraph lowers nothing" — so the summary lowered what the
    paragraph says it does not. Repaired by carrying that carve-out into the
    sentence in the paragraph's own words.
  - **"or `trivial`, where nothing a program executes or a caller reads as a
    contract is touched"** — checked and sound. It narrows the `If no` branch
    rather than overriding an earlier answer, and its wording is the
    `trivial` line's own, so it cannot disagree with it.
  - **"If yes, `critical`"** — checked and sound; it states the branch, and
    overrides nothing.
  What a reader does differently: a contributor editing a CI configuration
  file that also states rules contributors follow reads `critical` from the
  summary, which is what the clauses give, instead of being lowered to one
  pass by a sentence that was meant to cover pure process documents.
- R1.2 — note. It observed that the commit message claimed a record the tree
  did not yet carry. This description is that record, and it rests AC1's
  narrowing on the ticket's Notes and ADR-0004's Migration rather than on a
  fresh executor judgement.

### Out of scope (per ticket)
Confirmed; nothing here exceeds it.
- The five clauses — untouched, which AC3 shows.
- The `trivial` line and the process-document paragraph beneath it —
  untouched. R1.1's repair edits the process-document *sentence inside the
  block quote*, which is this ticket's Files, not the paragraph beneath the
  test.
- What any tier requires — unchanged; no tier's obligations move.

### How to verify
1. `sed -n '/^In one line:/,/answer above stands\.\*\*/p' docs/tier-review-model.md`
   — the summary as it now stands. Cover the clauses and run a CI workflow
   edit, a contract change, a case study and a rule added to
   `docs/quality-gates.md` through it; compare each with the clauses.
2. `git diff main...HEAD -- docs/tier-review-model.md` — one hunk, inside the
   block quote, which is AC3.
3. `sed -n '/^5\. \*\*Process surface/,/^$/p' docs/tier-review-model.md` —
   clause 5 as it stands, which the summary's new disjunct reproduces.

### Risks / follow-ups
- **The summary restates two rules and carries neither's falsifier.** It
  summarises the five clauses and the process-document paragraph, each of
  which has its own **Retired when:**, and it has one of its own beneath it.
  "Retiring a control" says a rule stated in two documents carries one
  falsifier at the place it is stated in full; this is one document, so the
  rule does not reach it, and the summary is expressly a summary. It is
  recorded because this is the third ticket to repair the summary after the
  clauses moved — EM-012-001 added the `trivial` outcome, EM-007-002 added the
  process-document sentence, and this one adds clause 5 and the carve-out. A
  fourth would be the second instance of a pattern that "A rule needs a second
  instance" would let someone write down: a summary that must be edited every
  time the thing it summarises changes has no site that goes red when it
  falls behind.

### Review
One independent review pass, per "The operative test" for a change to a
process document. No second pass is taken.

| Round | Must-fix | Where (rules / lists / documents / tests) | Inside previous round's fix | Repaired by |
|---|---|---|---|---|
| 1 | 1 (of 2 findings) | documents: the summary's closing sentence overrode the limb this ticket added with "whatever the answer", so a change that is both a process document and something a program executes returned `standard` where the clauses and the paragraph beneath the test return `critical` (must-fix); the commit message claimed a record of AC1's narrowing that the tree did not yet carry | — | 39e89dd |

Derived from the row and not asserted beside it: one must-fix over one review
round. Round 1 has no round before it, so its inside-previous-fix cell reads
`—` and no line is uncountable.

- R1.1 · permits · must-fix · `docs/tier-review-model.md`, the paragraph beneath the test, "A change that touches a process document and also something a program executes or a caller reads as a contract is classed by the rest of this test on that other thing; this paragraph lowers nothing" · the summary's "whatever the answer" lowered exactly that class to `standard`, defeating the limb this ticket had just added, determinately and in the opposite direction from the clauses — remedy: carry the paragraph's carve-out into the same sentence; cost, if the remedy tightens a control: a change editing a process document and in the same change a CI workflow, a migration or a schema moves from one pass to `critical`, which is already the clauses' answer, so the remedy imposes no control the test does not; on this repository the class is empty; inside previous fix: —
- R1.2 · permits · note · `docs/ai-contributor-policy.md` §6, "Every acceptance criterion met and demonstrated in the pull-request description, with evidence" · the commit message stated that AC1's overtaken half was recorded in the description while the description was still the authoring placeholder — remedy: write it at close, resting on the ticket's Notes and ADR-0004's Migration; cost: none; inside previous fix: —

The reviewer found nothing in the second column and recorded that as an
answer: the added disjunct reproduces clause 5's words exactly, so it
escalates nothing the clauses do not; it sits inside the `yes` branch, so the
`trivial` branch and the `standard` default are untouched; and a change to the
review model, which clause 5 now routes away, still lands at `standard`. It
noted that a finding against clause 5's flat treatment of CI changes would be
a finding against the clauses, which Out of scope holds, and declined to make
it.

### Definition of Done (all tiers)
The four machine checks do not apply to a repository that publishes documents
and runs no suite; the falsification gate is discharged above, with N/A for
the behavioural claim and a class line for the must-fix repaired. Every
measured figure names its baseline in the same sentence and is read from the
command named beside it. The independent pass a process-document change takes
has run and is recorded.
