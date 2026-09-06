---
id: EM-016
title: Bound the brief a contributor must read
status: done
tier: critical
complexity: M
dependencies: []
claimed_by: claude-fable-5-1
claimed_at: 2026-09-06
closed_at: 2026-09-06
---

# EM-016 — Bound the brief a contributor must read

## Context

The wave EM-006 to EM-014-001 took the five rule-bearing documents under
`docs/` from 3,152 words to 11,476, measured by `wc -w` at 8b0a8b4 and at
34dc12c. `docs/tier-review-model.md` alone went from 761 to 4,222 and now
carries eight sections. Every ticket in the wave priced its own addition
and none priced the total, because none could: the total is a property of
the set, not of any change in it.

The cost falls on two readers the documents name. The contributor policy's
§7 checklist requires an agent to have read that document end to end before
its first edit. A critical-tier reviewer is briefed from the tier review
model, and under "What a review reports" and "When review ends" must hold
the two questions, the three stopping conditions, the cap, the record's
fields and the class signal while reading a diff.

Nothing in the wave bounds this, and the model's own argument says why that
matters: an escalation everyone ignores is worse than none. A brief too
long to hold is skimmed, and a rule nobody reaches is a rule that does not
run. "Retiring a control" gives a rule a way out of the set; it gives the
reader no way through it.

The cheapest available remedy is not retirement, which needs evidence
against a particular rule, but navigation: say where each answer lives, so
that a reader reaches the governing rule without carrying the rest. This
repository already argues that redundant state which must agree is a cheap
and continuous integrity check — that is the directory/status invariant's
whole defence — and a map is the same shape of redundancy.

## Specification

Documentation changes only. No rule is retired, amended or added beyond the
one that keeps the map current.

### Files

- `docs/ai-contributor-policy.md` — an unnumbered section after the
  preamble and before §1, mapping each question to the document that
  settles it. No section is renumbered.
- `docs/tier-review-model.md` — an index of its own sections, after the
  opening paragraphs and before "The operative test".

### Public surface

N/A — this repository publishes documents. The change adds navigation and
one rule keeping it current, and removes nothing.

### Behaviour

- The policy's map names every rule-bearing document and the templates,
  gives for each the question it settles, and restates no rule. A reader
  with a question reaches one document rather than four.
- The map defers to §7 for what must be read before a first edit: it says
  where answers live, not what must be read.
- The model's index lists its sections in order with one line each saying
  what that section settles, and says which sections a critical-tier
  reviewer works from.
- **The rule this ticket adds:** a change that adds, removes or renames a
  section of a rule-bearing document updates the map and the index in the
  same commit. It is the directory/status invariant's argument applied to
  the documents: two descriptions that must agree make drift visible at no
  cost, and a stale map is worse than none.
- **The falsifier of that rule**, per "Retiring a control": retired when
  the map or the index is found stale by a review more than once over a
  stated population of merged changes — the same-commit rule is then not
  being followed, and a map nobody maintains costs a reader more than
  navigating without one.

## Acceptance criteria

1. AC1: `docs/ai-contributor-policy.md` carries a map naming every
   rule-bearing document under `docs/` and the templates, with the question
   each settles.
2. AC2: The map restates no rule, and defers to §7 for the reading
   obligation.
3. AC3: `docs/tier-review-model.md` carries an index of its sections,
   naming for each what it settles, and naming the sections a critical-tier
   reviewer works from.
4. AC4: The same-commit rule is stated once, in one of the two places, and
   referenced from the other; it carries a **Retired when:** line.
5. AC5: No section is renumbered and no existing rule's text changes. The
   diff to both documents is additive apart from the insertion points.
6. AC6: The pull-request description states, with its baseline: the word
   count of the five rule-bearing documents before and after; the count of
   sections the index covers; and the number of documents a reader must
   open to answer each mapped question, which should be one.
7. AC7: Critical tier per ADR-0002: an independent agent that did not
   perform the work reviews this against the artifacts and records findings
   in EM-010's two columns.

## Out of scope

- Retiring or amending any rule. The set is not shortened here; it is made
  navigable. Shortening it needs evidence against particular rules, which
  is what "Retiring a control" is for.
- Splitting any document into reference and operative halves. That is a
  larger change with its own argument, and this ticket is deliberately the
  cheaper one; if the map proves insufficient the split is the next ticket.
- Any change to §7's checklist or to what a reviewer receives.
- A summary of the rules. A summary is a second statement of every rule and
  would breach the no-restatement constraint every ticket in the wave
  observed; the map states none.

## References

- `docs/ai-contributor-policy.md` §7 — the reading obligation this map
  serves and does not change.
- `docs/tier-review-model.md`, the scrutiny-list section — "an escalation
  everyone ignores is worse than none", which is the hazard here.
- `docs/ticket-lifecycle.md`, "The directory/status invariant" — the
  argument the same-commit rule borrows.
- EM-014 and ADR-0003 — the falsifier obligation this ticket's new rule
  discharges.

## Notes

**On this ticket's tier.** Under the operative test as EM-012-001 leaves
it, a change to a document no program executes and no caller reads as a
contract is `trivial`; under ADR-0002 a change to a process document is
`critical`. The two disagree, and EM-007-002 owns that question. The tier
is proposed `critical` here because the executor may raise and may never
lower, so the conservative reading is the one an author can take without
resolving anything.

**Why a map and not a shorter set.** Every rule in the set was argued for
and reviewed, and this ticket has no evidence against any of them. The
honest complaint is not that the rules are wrong but that the reader cannot
find them, and that is a navigation defect with a navigation fix.

## PR Description

### Ticket
EM-016 — Bound the brief a contributor must read

### Tier
`critical` — process-surface change (clause 5): it adds a rule to the
contributor policy and navigation to two process documents.

**Independent review obtained**, per ADR-0002: a separate agent, given the
ticket, the diff and the two questions, and not the executor's reasoning,
reviewed the change in three rounds, read-only. Findings are under
Review; the tree was checked clean after each round.

### Summary
The contributor policy gains "Which document settles what", a table routing
each question to the place that settles it. The tier review model gains an
index of its nine sections. One rule keeps both current, naming the three
ways a map can be wrong and a trigger for each; it is stated once with the
map, referenced from the index, and carries its falsifier. No rule is
retired or amended and no section is renumbered.

### Acceptance criteria
- [x] AC1: a map naming every rule-bearing document and the templates, with
  the question each settles — `docs/ai-contributor-policy.md`, "Which
  document settles what", nine rows.
- [x] AC2: the map restates no rule and defers to §7 — "The table states no
  rule; each row names where the rule is. What you must read before your
  first edit is §7's checklist, not this table." The reviewer checked every
  row and found no cell that states a rule.
- [x] AC3: the model carries an index naming what each section settles and
  which sections a critical-tier reviewer works from —
  `docs/tier-review-model.md`, "What is in this document": three sections
  worked from, and "Separation of duties" binding whether or not the
  reviewer opens it.
- [x] AC4: the same-commit rule is stated once and referenced from the
  other place, with a **Retired when:** line — stated under "Keeping the
  map true" in the policy; the index closes with "The rule that keeps this
  index current is stated once, with the map in
  `docs/ai-contributor-policy.md`".
- [x] AC5: no section renumbered and no existing rule's text changed —
  `git diff -w e1beeb6..HEAD` removes nothing from either document. Three
  paragraphs of existing or added text were re-wrapped; all three are
  declared under Out of scope below.
- [x] AC6: figures below.
- [x] AC7: independent review — see Review.

### AC6 — the figures
`wc -w` on the five rule-bearing documents, at 8b0a8b4 (the wave's
baseline), at e1beeb6 (this ticket's baseline) and at close:

| Document | 8b0a8b4 | e1beeb6 | close |
|---|---|---|---|
| `ai-contributor-policy.md` | 1,034 | 2,316 | 2,899 |
| `tier-review-model.md` | 761 | 4,222 | 4,461 |
| `quality-gates.md` | 411 | 2,229 | 2,229 |
| `ticket-lifecycle.md` | 544 | 2,153 | 2,153 |
| `adr-process.md` | 402 | 563 | 563 |
| **Total** | **3,152** | **11,483** | **12,305** |

The baseline for this change is e1beeb6, 11,483 words, and not the 11,476
the ticket's Context quotes at 34dc12c: EM-017 added seven words to the
lifecycle between the two. This change adds 822 words, all to the two
documents it edits.

The index covers 9 sections against the 9 `## ` headings in the document,
its own included. That was the first application of the rule it sits
beside, and round 1 caught it failing: the index shipped covering 8 of 9.

Each of the map's nine rows names the place that settles its question, and
the reviewer checked every row. Round 1 found two that did not. The
merge-conditions row sent a reader to the quality gates while §6 carries
the rest of the definition of done; and the tier model's row completes only
with the decision-record process for what a retirement record carries. Both
are answered by rows of their own now.

**Who pays and who is paid.** For the reader §7 obliges to read the policy
end to end before a first edit, this change is strictly longer: 2,316 to
2,899 words, a quarter again, and the map is read before that document rather than instead
of it. The saving goes to the returning reader with a question, who reads
one row instead of searching five documents. The ticket chose navigation
over shortening and argued for it; this is the direction of the number, and
it is not a saving for everyone.

### Falsification
N/A — no behavioural claim. What a reader does differently, per criterion:
- AC1, AC2: a reader with a question reads one row and goes to the place
  that settles it, instead of searching five documents.
- AC3: a reviewer briefed for a critical-tier change knows which sections
  carry the review rules and which binds it unread.
- AC4: an author who adds a document, moves where a question is settled, or
  adds a section to an indexed document updates the map or that index in
  the same commit, as they already do for a ticket's directory and status.
- AC5, AC6: nothing; they are the guards.

Repairs of this review's findings, in the class form policy §6 asks for.
There is no suite here, so each sibling says what a reader would do
differently.
- R1.2 and R1.4 — class: **what change can make the map or an index wrong,
  and does the rule fire on exactly those?** Siblings, from the reviewer's
  enumeration: a section added, removed or renamed (fired, but demanded a
  map edit that most section changes cannot supply — now fires on the
  index always and the map only where a row's question changes); a document
  added, removed or renamed (did not fire — now does); a document's scope
  moving so a row's question is answered elsewhere (did not fire — now
  does); a section in a document the map does not list (did not fire, by
  design — now stated, so a reader is not left guessing). Red, in the sense
  available here: before the repair an executor adding a section to the
  quality gates had no achievable map edit and would have had to block on
  its own rule.
- R1.1 — repair of the instance: the index omitted its own section. One
  row.
- R1.3 — repair of the instance: one row's question was answered in two
  places. One row added, and the premise no longer claims one document per
  question.
- R1.6, R1.10 — repair of the instance, each: one sentence.

### Out of scope (per ticket)
Confirmed: no rule retired or amended; no document split into reference and
operative halves; §7's checklist and what a reviewer receives are
untouched; no summary of the rules — every map cell is a question or a
path.

Beyond the Files list and declared here, all whitespace, no word changed:
a 118-character line in §3 left by the close of EM-008, re-flowed in
`0bd6aef` and declared in that commit; a paragraph of `docs/tier-review-model.md`
re-wrapped inside `3e37d70` without cause and undeclared until now, which
round 1 found (R1.5); and the index's own paragraph re-flowed in `dc3b437`
after the round-1 repair ran it long.

Recorded, not changed (R1.8): the map's questions are in the first person
— "What may I do", "what does the falsification gate ask of me?" — against
§1's "Never write 'I' or 'we' in a committed file". The precedent is §7's
own checklist, which is written the same way; §1's target is the author's
session voice, and this is the reader's. Left as it stands, and named here
so a reader who notices finds it decided rather than missed.

### Review
| Round | Must-fix | Where (rules / lists / documents / tests) | Inside previous round's fix | Repaired by |
|---|---|---|---|---|
| 1 | 4 (of 10 findings) | documents: the index omitted its own section, so the rule failed on its first application (must-fix); the same-commit trigger did not fire on a document added, removed or renamed (must-fix); a map row sent a reader to the quality gates while §6 carries the rest of the definition of done (must-fix); the trigger demanded a map edit most section changes cannot supply (must-fix); an undeclared re-flow; the reviewer's sections understated; the direction of the word count; first person in the map's questions; the README's table unbound; two rows overlapping on blocking | — | 65c652f, dc3b437 |
| 2 | 1 (of 3 findings) | documents: the exemption clause swallowed the document trigger, since a new document has no row by definition (must-fix); the narrowed gates row still caught a reader asking about merge; EM-016-001 permitted a route its trivial tier was not argued for | 3 of 3 | 8c5bbaa |
| 3 | 0 (of 1 note) | documents: no row asks where a review runs | 1 of 1 | the closing commit |

Derived total: 5 must-fix over three rounds.
Round 1 by column and rule — permits: R1.1, this rule (the index omitted
its own section; remedy: one row); R1.2, this rule (the trigger missed a
document added, removed or renamed; remedied as a class with R1.4); R1.3,
the map's routing claim (a row sent a reader to one document while another
carried the rest; remedy: a row of its own, and the premise no longer
claims one document per question); R1.5, policy §2 (an undeclared re-flow;
recorded above); R1.8, policy §1 (first person in the map's questions;
recorded above, not changed); R1.9, this rule (the README's table is a
third description; raised as EM-016-001); R1.10, the map's routing claim
(two rows overlapping on blocking; remedy: three words). Refuses: R1.4,
this rule (the section trigger demanded a map edit most section changes
cannot supply, leaving an executor to block on the rule itself; remedied as
a class with R1.2 — a loosening); R1.6, the index's reviewer claim (it
understated what a reviewer works from and omitted what binds it unread);
R1.7, the ticket's own premise (the description must state who pays;
stated above).

Round 2 by column and rule — permits: R2.1, this rule, inside round 1's own
fix (the exemption clause swallowed the trigger it sat beneath, because a
newly added document has no row by definition; remedy: governance turns on
what a document does, with the executor's judgement stated rather than
hidden); R2.2, the map's routing claim, inside R1.3's fix (the narrowed
gates row still caught a reader asking about merge); R2.3, the operative
test, inside R1.9's fix (EM-016-001 permitted a route its trivial tier was
not argued for; remedy: scoped to the route, with the other named as
critical work and its own ticket).

Round 2's reviewer named the both-columns-on-one-rule signal as close, and
recorded why it did not fire: R1.2 and R2.1 are both first-column findings
on the same rule, and the signal turns on opposite columns in consecutive
rounds. It stated the alternative assignment so that the judgement could be
checked rather than taken. Round 3 found no finding on that rule in either
column, and its one note — no row asked where a review runs — is taken in
the closing commit.
Post-review tree check after each round: `git status --porcelain` empty,
`git worktree list` showing only the main tree.

### How to verify
1. `grep -c "^## " docs/tier-review-model.md` against the index's row
   count — the index covers every section, its own included.
2. For each map row, open the named place and find the question answered
   there.
3. `git diff -w e1beeb6..HEAD` — nothing is removed from either document.

### Risks / follow-ups
- **EM-016-001** (raised here, R1.9): the README's "Start here" table is a
  third description of the same documents, is not a row of the map, and is
  already behind.
- The map is a second description of the document set, and the rule that
  keeps it true is the only thing between it and staleness. Its falsifier
  says what staleness would look like; the first document or section added
  after this lands is the first test, and round 1 showed the rule can fail
  in the commit that states it.
- This ticket makes the set navigable and does not make it smaller. If a
  reader still cannot hold the brief, the next lever is separating each
  document's rules from its reasoning, which the Out of scope names and
  does not take.

