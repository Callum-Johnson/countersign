---
id: EM-016-001
title: The README's document table is a third description the same-commit rule does not bind
status: in-progress
tier: trivial
complexity: S
dependencies: [EM-016]
claimed_by: claude-fable-5-1
claimed_at: 2026-09-06
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
- The table is named in the map's rows, so that it is bound like the
  others and stops being a third description nothing keeps true. Extending
  the map's rule instead would edit a rule in
  `docs/ai-contributor-policy.md`, which is a process-surface change and
  not this ticket's; if the implementer judges the rule needs extending,
  that is a separate ticket at `critical` tier.
- No rule is stated in the README that is not stated in the document the
  row names.

## Acceptance criteria

1. AC1: every row of `README.md`'s "Start here" table matches what its
   document settles at close.
2. AC2: the table is named in the map's rows, and so bound by the
   same-commit rule in `docs/ai-contributor-policy.md`, "Which document
   settles what".
3. AC3: the README states no rule the named document does not.

## Out of scope

- Any other part of `README.md`, including the core ideas.
- Any change to the map's rule, or to the index. Adding the row the map
  needs is not a change to the rule.
- Extending the same-commit rule's wording. That is `critical` work and its
  own ticket.

## References

- EM-016 — the map, the index, and the rule this table escapes.
- `README.md`, "Start here".

## Notes

Trivial by the operative test as EM-012-001 leaves it: a table of links in
a document no program executes and no caller reads as a contract, plus one
row added to a table. The tier is argued for that work only, which is why
the rule-extension route is out of scope above; a ticket that edited the
rule would be `critical` and the executor may raise but never lower. The tier
question EM-007-002 owns applies here as it does to every documentation
ticket on this board.

## PR Description

### Ticket
EM-016-001 — The README's document table is a third description the
same-commit rule does not bind

### Tier
`trivial` — a table of links in `README.md` and one row added to a table
in `docs/ai-contributor-policy.md`; no clause of the operative test holds
and nothing a program executes or a caller reads as a contract is touched.
The rule under "Keeping the map true" is not edited: `git diff -w ce59c8f
HEAD -- docs/ai-contributor-policy.md` adds one line and removes none. No
independent review at this tier; the author self-merges, per the tier
table.

### Summary
Each row of the README's "Start here" table now says what its document
settles, written from the policy's map, the tier model's index and the
documents' own sections. The map gains a row naming the table, so that the
same-commit rule binds it as it binds the model's index; the rule's wording
is unchanged.

### Acceptance criteria
- [x] AC1: every row of `README.md`'s "Start here" table matches what its
  document settles at close — each row was written from, and can be checked
  against, these sections: the policy's "Which document settles what", §3,
  §6 and §7; the lifecycle's "The directory/status invariant", "Claiming",
  "Batching trivial work", "Blocking", "Closing" and "Lineage"; the tier
  model's index, "What is in this document", whose nine rows the README row
  condenses; the quality gates' opening block, "The falsification gate" and
  "Review isolation"; the decision-record process's "When to write one",
  "Structure" and "Decisions about the process are themselves ADRs"; and
  `DISCLOSURE.md`'s "The short version" and "What is published". The table
  has 6 rows at 02a7ebe and had 6 at ce59c8f, by `grep -c '^| \['
  README.md`: no row was added or removed.
- [x] AC2: the table is named in the map's rows — the last row of "Which
  document settles what" asks where to start and what each document settles
  in a line, and names `README.md`, "Start here", as an index of the
  documents. The map has 10 rows at 02a7ebe against 9 at ce59c8f, by
  `grep -c '^| [^|]*? |' docs/ai-contributor-policy.md`. The rule binds it
  by its own terms: "This rule governs every document the map names", and
  "the map and the indexes it governs" reaches a row that names an index.
- [x] AC3: the README states no rule the named document does not — each
  cell names what its document settles, and every phrase in it is the
  subject of a section listed under AC1; none states what a contributor
  must do. The one phrase with a rule's shape, "the four machine checks
  that must pass before merge", is the quality gates' own first sentence.

### Falsification
N/A — no behavioural claim. What a reader does differently, per criterion:
- AC1: a reader choosing a document from the README reaches the one that
  settles the question — the tier model for when a review ends or how a
  rule leaves, the policy for what must be true before a change is reported
  done — instead of learning on arrival that the row undersold it. At
  ce59c8f the tier model's row named three of the nine things its index
  lists.
- AC2: an author who adds a governed document, or moves where a question is
  settled, updates the README's table in the same commit as the map,
  because the map now names it. Before, the table was outside the rule and
  drifted silently.
- AC3: nothing; it is the guard. A reader who takes a row for a rule finds
  the rule where the row points.

### Out of scope (per ticket)
Confirmed: the core ideas and every other section of `README.md` are
unchanged — `git diff ce59c8f HEAD -- README.md` is 12 changed lines, six
removed and six added, all inside the table; the map's rule paragraph and
the model's index are untouched; the rule's wording is not extended.

Beyond the Files list and declared here: `docs/ai-contributor-policy.md`,
one row. The ticket's Files names `README.md` only, while its Behaviour,
AC2, Out of scope and Notes each call for the row; the four agree on what
is done and the Files list is short by one entry, so the edit is declared
rather than blocked on, as EM-020's description declared its index row.

Left as it stands: the table's column header, "What it covers". The
ticket's Behaviour speaks of what each document settles; the header
describes the column and states no rule, and changing it is not asked for.

Recorded, not changed: `README.md`, core idea 4, states the operative test
with two tiers where the model has three. It is the ticket's Out of scope
and is raised as EM-016-001-001.

### How to verify
1. For each row of `README.md`, "Start here", open the named document and
   find each phrase of the row settled by one of the sections listed under
   AC1.
2. `grep -c '^| [^|]*? |' docs/ai-contributor-policy.md` — 10; the last
   row names `README.md`, "Start here".
3. `git diff -w ce59c8f HEAD -- docs/ai-contributor-policy.md` — one line
   added, none removed. `git diff ce59c8f HEAD -- README.md` — six lines
   replaced, all between the table's header and `Templates are in`.

### Risks / follow-ups
- **EM-016-001-001** (raised here): core idea 4 names two tiers of three.
- The table is bound through a row and the words "an index of the
  documents", not through the rule's triggers by name. If a later change
  finds the triggers do not reach the table without extending the rule's
  wording, that is the `critical` ticket this ticket's Out of scope names.
  The first governed document added or moved after this lands is the first
  test.

### Review
N/A — trivial tier.
