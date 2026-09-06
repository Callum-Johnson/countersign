---
id: EM-016-001
title: The README's document table is a third description the same-commit rule does not bind
status: ready
tier: trivial
complexity: S
dependencies: [EM-016]
---

# EM-016-001 — The README carries a third description of the documents

## Context

Raised by the independent review of EM-016 (finding R1.9 of round 1),
created on the branch under review per `docs/ticket-lifecycle.md`,
"Lineage".

EM-016 adds a map in `docs/ai-contributor-policy.md` and an index in
`docs/tier-review-model.md`, with one rule keeping both current.
`README.md`'s "Start here" table is a third description of the same five
documents, is not a row of the map, and is therefore not bound by that
rule. It is already behind: its row for the tier review model reads "Three
risk tiers, the operative test that assigns them, and what each demands",
and that document now also settles what a review reports, when review ends,
and how a rule leaves the documents.

A maintained redundancy beside an unmaintained one is the drift the map was
added to make visible, one level out.

## Specification

Documentation change only.

### Files

- `README.md` — the "Start here" table.

### Public surface

N/A — this repository publishes documents. No rule changes; one table is
brought up to date and placed under an existing rule.

### Behaviour

- Each row of the README's table describes what that document settles as it
  now stands.
- The table is named in the map's rows, or the map's rule is extended to
  reach it, so that it is bound like the others. Which of the two is the
  implementer's judgement; the requirement is that it stops being a third
  description nothing keeps true.
- No rule is stated in the README that is not stated in the document the
  row names.

## Acceptance criteria

1. AC1: every row of `README.md`'s "Start here" table matches what its
   document settles at close.
2. AC2: the table is bound by the same-commit rule in
   `docs/ai-contributor-policy.md`, "Which document settles what", by
   whichever of the two routes the implementer takes.
3. AC3: the README states no rule the named document does not.

## Out of scope

- Any other part of `README.md`, including the core ideas.
- Any change to the map or the index themselves.

## References

- EM-016 — the map, the index, and the rule this table escapes.
- `README.md`, "Start here".

## Notes

Trivial by the operative test as EM-012-001 leaves it: a table of links in
a document no program executes and no caller reads as a contract. The tier
question EM-007-002 owns applies here as it does to every documentation
ticket on this board.

## PR Description

> Leave this section empty when authoring the ticket.
