---
id: EM-012-001
title: The tier model does not say how trivial is distinguished from standard
status: in-progress
tier: critical
complexity: S
dependencies: [EM-012]
claimed_by: claude-fable-5-1
claimed_at: 2026-09-06
---

# EM-012-001 — The tier model does not say how trivial is distinguished from standard

## Context

Raised by the independent review of EM-012 (finding R1.2 of round 1). The
operative test in `docs/tier-review-model.md` has two outcomes: any clause
holds, `critical`; none holds, `standard`. The tier table has three rows.
`trivial` is assigned only by the table's "Typical work" column —
documentation, comments, data additions, ticket edits — and nothing states
the test that separates it from `standard`. EM-012's batch path admits "a
change whose tier is `trivial`", and an adopter listing entries with "the
operative-test answer that supports it" can write only that no clause
holds, which is the `standard` answer too.

EM-012's Out of scope reserves "any change to the operative test, or to
what `trivial` means"; the gap is recorded here rather than closed there.

## Specification

Documentation change only.

### Files

- `docs/tier-review-model.md` — "The operative test" or "The tiers".

### Public surface

N/A — this repository publishes documents. The change states a test that
the table already implies.

### Behaviour

- The model states, in one or two sentences, the test that returns
  `trivial` where the operative test returns `standard`: a change that no
  code path executes and no contract reads — documentation, comments, data
  a program does not load, ticket files — is `trivial`; anything a program
  or a caller can observe is at least `standard`.
- The sentence says who decides where the line is unclear: the executor
  may raise, never lower, as the separation-of-duties section already
  says.
- The rule states its falsifier, per "Retiring a control".

## Acceptance criteria

1. AC1: `docs/tier-review-model.md` states a yes/no test for `trivial`.
2. AC2: The test is consistent with the table's "Typical work" column and
   changes no row's review requirement.
3. AC3: The rule carries a Retired-when line.
4. AC4: Critical tier per ADR-0002: an independent agent reviews this
   against the artifacts and records findings in two columns.

## Out of scope

- Changing what the operative test returns `critical` for.
- Changing any tier's review requirement.

## References

- `docs/tier-review-model.md`, "The operative test" and "The tiers".
- EM-012 — the batch path that needs the test, and its Out of scope.
- ADR-0001, Alternative 3 — "trivial-tier work needs a ticket but no
  review", which assumes the tier can be told.

## Notes

Critical under the operative test's process-surface clause: the tier model
is the review model.

## PR Description

> Leave this section empty when authoring the ticket.
