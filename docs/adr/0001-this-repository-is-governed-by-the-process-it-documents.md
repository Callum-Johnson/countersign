# ADR-0001: This repository is governed by the process it documents

- **Status:** accepted
- **Date:** 2026-08-31
- **Deciders:** maintainer
- **Related:** EM-003 (this decision); ADR-0002 (the single-maintainer problem
  it creates); DISCLOSURE.md

## Context

This repository documents a ticket lifecycle, a review model, and an AI
contributor policy, and asserts that they were applied continuously to a
private project.

Until now it did not apply them to itself. The initial commit landed 24 files
and 2,540 lines with no ticket, no decision record, and no acceptance
criteria. That is verifiable in the git history and would be the first thing a
sceptical reader checks.

A repository whose only claim is "here is how I work" and whose own history
shows something else is not evidence. It is a brochure.

There is a second, less obvious problem. Documented process and practised
process drift apart, and the direction is always the same: the document
describes what you meant to do. Applying the process here means every
inaccuracy in the documents becomes something that obstructs actual work, and
therefore gets found.

## Decision

All work on this repository from this commit forward goes through the process
this repository documents: a ticket file before the work, the directory/status
invariant, the tier model, a pull-request description with evidence per
acceptance criterion, and a decision record where the decision is
architectural.

The identifier prefix is `EM`. Lineage follows the documented scheme:
`EM-004-001` is a ticket raised while working `EM-004`.

**The initial commit is not retrofitted.** No ticket is backdated to describe
work that was done without one. Two tickets covering that work exist in
`done/` and both state plainly that they were written after the fact.

## Rationale

Backdating would have been easy and is the obvious temptation. It is rejected
for the reason the whole repository exists: the artifacts have to be real or
they are worth nothing. A reader who diffs the ticket dates against the commit
dates and finds them fabricated learns something true and fatal about
everything else here.

Recording the adoption as a decision costs one ADR and converts an
embarrassment into the clearest possible demonstration of the practice: this
is what it looks like when the process catches its own absence.

## Consequences

- **Positive:** the repository's git history becomes primary evidence rather
  than a liability. The claim is checkable.
- **Positive:** documented process is now load-bearing here, so drift between
  the documents and the practice surfaces as friction rather than silently.
- **Negative:** overhead is real and disproportionate at this size. A
  documentation change now needs a ticket. This is accepted deliberately; a
  process only applied when convenient is not a control.
- **Negative:** the tier model's critical-review requirement cannot be met by
  a single maintainer. See ADR-0002.
- **Neutral:** the first two tickets in `done/` are retrospective and say so.

## Alternatives considered

### Alternative 1: Backdate tickets for the initial commit

Write tickets for the work already done, dated to match. Rejected: it is
fabrication, it is trivially detectable by comparing file dates to commit
dates, and being caught at it would discredit the genuine artifacts in
`examples/` by association.

### Alternative 2: Leave the repository ungoverned

Document the process, do not apply it. Rejected: it is the weakness this ADR
exists to fix. A reviewer's first question about a methodology repository is
whether the author uses it.

### Alternative 3: Apply the process only to substantive changes

Exempt documentation edits and typo fixes. Rejected as the standard failure
mode: "substantive" is decided by the person who wants the exemption, and the
exemption widens. The tier model already handles this properly — trivial-tier
work needs a ticket but no review.

## Migration

EM-003 creates the ticket directories, the decision-record directory, and the
retrospective tickets. No existing content changes.
