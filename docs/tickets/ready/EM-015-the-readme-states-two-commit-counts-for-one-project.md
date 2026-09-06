---
id: EM-015
title: The README states two commit counts for one project
status: ready
tier: trivial
complexity: S
dependencies: []
---

# EM-015 — The README states two commit counts for one project

## Context

Found on 2026-09-06 during an assessment of the repository at 0947dda, by
grepping every figure the README asserts against the case study it summarises.

`README.md` says, in "Why this exists", that the process was applied to a
codebase that reached **1,879** commits in two months. The table under "Where
this came from" in the same file, and `case-studies/00-growth-2024-2026.md` in
two places, give the same project **2,294** commits. Both figures landed in
the initial commit; neither names the date it was counted.

This is the defect EM-006 describes in its Notes — a figure inherited and
restated without its baseline — occurring in the first paragraph a reader
sees. Either figure may be true at a different date; the README does not say
which, and a reader who notices learns something about every other number in
the repository.

## Specification

Documentation change only.

### Files

- `README.md` — the sentence in "Why this exists".

### Behaviour

- The README gives one commit count for the project, and it is the count the
  case study gives, or the two are made to agree at a stated date.
- The sentence names the date or commit the count was taken at, per the
  baseline rule EM-006 introduces, so that the next drift is visible.

**Only the maintainer can supply the figure.** The private repository is the
only place it can be counted, and the executor that raised this ticket cannot
count it. The ticket is in `ready/` because the change is fully specified;
the input it needs is one number and its date.

## Acceptance criteria

1. AC1: `grep -n "1,879\|2,294" README.md case-studies/*.md` returns one
   figure, or two figures each with a stated date.
2. AC2: The README sentence names when its count was taken.

## Out of scope

- Any other figure in the README or the case study. This ticket is one
  sentence; if the audit finds more, they are their own ticket.

## References

- `README.md`, "Why this exists" and "Where this came from"
- `case-studies/00-growth-2024-2026.md`, the table and the rules-engine section
- EM-006, Notes — "a measured number and an inherited one are
  indistinguishable once written down"

## Notes

Trivial tier under the operative test: no rule, procedure or template
changes; one figure in one sentence.

## PR Description

> Leave this section empty when authoring the ticket.
