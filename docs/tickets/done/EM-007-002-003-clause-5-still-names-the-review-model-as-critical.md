---
id: EM-007-002-003
title: Clause 5 of the operative test still names a change to the review model as critical
status: done
tier: standard
complexity: S
dependencies: [EM-007-002]
claimed_by: claude-opus-5
claimed_at: 2026-09-15
closed_at: 2026-09-15
---

# EM-007-002-003 — Clause 5 still names the review model as critical

## Context

Raised while working EM-007-002, under the contributor policy's §4, from
the one independent pass on that ticket (finding R5.2). Clause 5 of "The
operative test" in `docs/tier-review-model.md` — "A schema migration, a CI
configuration change, or a change to the review model itself" — sits under
the heading "Any one clause means `critical`", while the paragraph beneath
the test, landed by EM-007-002 under ADR-0004, makes a change to the review
model `standard` on one pass, the review model being a process document.
The two are reconciled only by the paragraph's own sentence claiming
precedence over the clause; a contributor who reads the clauses and stops
gets `critical`. EM-007-002's Out of scope excluded any change to the five
clauses, so the contradiction is left in the clause's words and this ticket
takes it.

## Specification

Documentation change only. `docs/tier-review-model.md`, "The operative
test", clause 5: amend its words so that they no longer name a change to
the review model, or so that they send such a change to the paragraph that
decides it, leaving a schema migration and a CI configuration change
`critical` as they are. No new rule is added; the clause retires with the
line already beneath the test. EM-007-002-001 works the one-line summary's
`critical` limb; this ticket works the clause, and the two do not overlap.

## Acceptance criteria

1. AC1: clause 5, read on its own, no longer returns `critical` for a
   change to the review model itself.
2. AC2: a schema migration and a CI configuration change still return
   `critical` under clause 5.
3. AC3: the paragraph beginning **A change to a process document** is
   unchanged, and its precedence sentence over clause 5 is either removed as
   no longer needed or left agreeing with the clause's new words.
4. AC4: one independent review pass, recorded as one row of the Review
   table, per "The operative test".

## Out of scope

- Clauses 1 to 4.
- The process-document paragraph and what any tier requires.
- The one-line summary, which is EM-007-002-001.

## References

- `docs/tier-review-model.md`, "The operative test", clause 5 and the
  paragraph beneath the test.
- ADR-0004, Consequences, the neutral bullet naming this clause.
- EM-007-002, Review, R5.2 — the finding this ticket is raised from.

## Notes

N/A

## PR Description

### Ticket
EM-007-002-003 — Clause 5 of the operative test still names a change to the
review model as critical.

### Tier
`standard`, on one independent review pass. A change to
`docs/tier-review-model.md` is a change to a process document, which "The
operative test" fixes at that tier — the paragraph this ticket makes clause 5
point at. The pass ran against d7b04f5 and is row 1 of the Review table.

### Summary
Clause 5 sat under "Any one clause means `critical`" while naming a change to
the review model, which ADR-0004 makes `standard` on one pass. The two were
reconciled only by a sentence further down claiming precedence, so a
contributor who read the clauses and stopped got the wrong tier. Clause 5 now
names a schema migration and a CI configuration change only, and routes a
review-model change to the paragraph that decides it.

### Acceptance criteria
- [x] AC1: clause 5, read on its own, no longer returns `critical` for a
  change to the review model itself — it names a schema migration or a CI
  configuration change as its trigger, then says of a review-model change
  that the process-document paragraph and the tier it states "decide that;
  this clause does not". The disclaimer is in the clause's own words rather
  than left to a sentence further down.
- [x] AC2: a schema migration and a CI configuration change still return
  `critical` under clause 5 — they stand as the clause's first sentence,
  under the same heading, unqualified.
- [x] AC3: the paragraph beginning **A change to a process document** is
  unchanged — `git diff main...HEAD -- docs/tier-review-model.md` shows two
  hunks, neither touching it. The precedence sentence, which lives in the
  next paragraph, is kept and shortened to the cross-reference alone, which
  is AC3's second arm: it agrees with clause 5's new words and no longer
  restates the fact clause 5 now states.
- [x] AC4: one independent review pass, run against d7b04f5 by an agent that
  did not perform the work and did not receive the executor's reasoning,
  recorded as row 1 of the Review table below. It returned one must-fix over
  three findings, repaired at b1d60aa.

### Falsification
N/A for a behavioural claim — this repository publishes documents and the
change adds no behaviour. Per criterion, what a reader does differently: a
contributor running the operative test against a change to the review model
reads clause 5, is told in the clause that it does not decide, and follows
the pointer to the paragraph that does, instead of stopping at `critical`.

For the review finding repaired, per the contributor policy's §6:
- R1.1 — class: **which statements elsewhere describe clause 5's words, and
  stop holding when those words change?** ADR-0004's Consequences neutral
  bullet is the instance. The question was asked of the tree by `grep -rn
  "review model itself" --include=*.md docs templates`, run after b1d60aa.
  Siblings, each checked:
  - **ADR-0004's neutral bullet** — the instance. It said the clause "still
    names" the review model and that its words "are unchanged", both false
    after d7b04f5. Repaired by annotation below a horizontal rule, in the
    form ADR-0002 and ADR-0003 already carry, quoting the clause as it stood
    and as it now reads. The text above the rule and the status are
    untouched, so the decision is not rewritten.
  - **The operative test's one-line summary** — checked and sound. It was
    already narrowed to a CI configuration change and a schema migration, and
    naming the review model is the limb EM-007-002-001 owns; this change
    leaves it no staler than it was.
  - **The closed record of EM-007-002, and this ticket's own Context** —
    checked and correctly left. Both quote the clause as it stood, which is
    what a record does; closed descriptions are not rewritten.
  What a reader does differently: a reader of ADR-0004 who reaches the
  neutral bullet is told, in the same record, that the clause has since been
  amended and what it now says, instead of carrying away a false picture of
  the clause the record is about.
- R1.2 — note. Repaired in the round; a note carries nothing under §6 as
  EM-009-001 narrowed it.
- R1.3 — note. Repaired in the round, on the same footing.

### Out of scope (per ticket)
Confirmed; nothing here exceeds it.
- Clauses 1 to 4 — untouched.
- The process-document paragraph and what any tier requires — untouched. The
  paragraph edited is the raise-never-lower one, and only its cross-reference
  sentence moved, which AC3 authorises.
- The one-line summary, which is EM-007-002-001 — untouched.

### How to verify
1. `sed -n '/^## The operative test/,/^If none hold/p' docs/tier-review-model.md`
   — the five clauses as they now stand. Run clause 5 alone against a change
   to `docs/tier-review-model.md` and against a schema migration, and check
   the two answers differ.
2. `git diff main...HEAD -- docs/tier-review-model.md` — two hunks, neither in
   the paragraph beginning **A change to a process document**.
3. `grep -rn "review model itself" --include=*.md docs templates` — two sites,
   clause 5 and ADR-0004's annotated bullet, and no third.
4. `sed -n '/^## Annotation/,$p' docs/adr/0004-a-process-document-change-is-standard-on-one-pass.md`
   — the annotation, below the rule, with the status untouched above it.

### Risks / follow-ups
- **Routed, not repaired.** ADR-0004 reads `status: proposed` while the
  commits that landed it are on `main`, and `docs/adr-process.md` says the
  status "becomes `accepted` when the change merges". The round-1 reviewer
  recorded this as an observation outside the change rather than a finding,
  and it is outside this ticket's Files. EM-007-002-003-001 owns it.
- The annotation is the third on a decision record in this repository, after
  ADR-0002's and ADR-0003's. If a fourth is needed for the same reason — a
  later ticket amending words an earlier record quotes — that is a second
  instance of a pattern, and "A rule needs a second instance" would let
  whoever meets it write the practice down rather than leave it as worked
  examples.

### Review
One independent review pass, per "The operative test" for a change to a
process document. No second pass is taken.

| Round | Must-fix | Where (rules / lists / documents / tests) | Inside previous round's fix | Repaired by |
|---|---|---|---|---|
| 1 | 1 (of 3 findings) | documents: ADR-0004's Consequences neutral bullet states that clause 5 still names a change to the review model and that its words are unchanged, both falsified by this change, in the record the ticket's own References send the executor to (must-fix); the kept precedence sentence restates the categorical fact clause 5 now states, two sites free to drift; clause 5's pointer named the paragraph that defines a process document, which decides nothing, rather than the one stating the tier | — | b1d60aa |

Derived from the row and not asserted beside it: one must-fix over one review
round. Round 1 has no round before it, so its inside-previous-fix cell reads
`—` and no line is uncountable.

- R1.1 · permits · must-fix · `docs/adr/0004-a-process-document-change-is-standard-on-one-pass.md`, Consequences, the neutral bullet · the bullet says clause 5 "still names" a change to the review model and that "the clause's words are unchanged, being outside EM-007-002's scope"; this change makes both false, and the ticket's References send the executor to that bullet, so it was in reach — remedy: a dated annotation below a horizontal rule, in the form ADR-0002 and ADR-0003 carry, quoting the clause as it stood and as it now reads, with the text and status above the rule untouched; cost, if the remedy tightens a control: none, it corrects one restatement in one record and adds no refusal; inside previous fix: —
- R1.2 · permits · note · `docs/tier-review-model.md`, the kept precedence sentence · clause 5's new second sentence states that the review model is a process document, so the kept sentence is a second statement of the same fact, in the shape that produced this ticket — remedy: shorten it to the cross-reference alone; cost, if the remedy tightens a control: none; inside previous fix: —
- R1.3 · permits · note · `docs/tier-review-model.md`, clause 5's pointer · the paragraph named defines a process document and decides nothing; the tier is stated in the paragraph after it, which carries no bolded name, so a reader following the pointer literally reaches a definition — remedy: point at that paragraph and the tier it states; cost, if the remedy tightens a control: none; inside previous fix: —

The reviewer found nothing in the second column and recorded that as an
answer rather than leaving the column empty: the change removes one limb from
a `critical` trigger and adds a routing sentence, so it adds no refusal for
honest work to pay. It checked that a process-document change that is not the
review model still reaches the same answer, that a change touching both the
review model and something a program executes is still classed on that other
thing, and that a schema migration and a CI configuration change are
untouched.

### Definition of Done (all tiers)
The four machine checks do not apply to a repository that publishes documents
and runs no suite; the falsification gate is discharged above, with N/A stated
for the behavioural claim and the class line given for the one must-fix
repaired. Every measured figure names its baseline in the same sentence and is
read from the command named beside it. The independent pass a process-document
change takes has run and is recorded.
