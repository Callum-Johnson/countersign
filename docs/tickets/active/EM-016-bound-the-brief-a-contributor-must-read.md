---
id: EM-016
title: Bound the brief a contributor must read
status: in-progress
tier: critical
complexity: M
dependencies: []
claimed_by: claude-fable-5-1
claimed_at: 2026-09-06
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

> Leave this section empty when authoring the ticket.
