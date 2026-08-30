# ADR-0002: Critical-tier review in a single-maintainer repository

- **Status:** accepted
- **Date:** 2026-08-31
- **Deciders:** maintainer
- **Related:** ADR-0001 (adopting the process here); docs/tier-review-model.md

## Context

ADR-0001 adopts the tier review model for this repository. The model requires
that critical-tier work receive one approval from **a reviewer who is not the
executor**, and that the reviewer verify the evidence independently rather than
accept the executor's summary.

This repository has one maintainer.

The requirement is not incidental. It is the enforcement mechanism behind the
separation-of-duties rule — that only a reviewer may lower a tier the executor
raised — and that rule is the part of the model most worth having. Declaring
the requirement inapplicable here would hollow out the model in exactly the
place a reader should test it hardest.

Changes to process documents are process-surface changes, which the operative
test classifies as critical. So this is not a rare case: on a repository whose
content *is* process documentation, most substantive work is critical tier.

## Decision

Critical-tier work in this repository requires review by **an independent
agent that did not perform the work**, given the ticket and the diff but not
the executor's reasoning. The reviewer verifies each acceptance criterion
against the artifact itself and records findings in the pull-request
description.

The reviewer may be an AI agent. It may not be the agent that did the work,
and it may not be given the executing agent's session context — that is what
makes it independent rather than a second opinion from the same reasoning.

Where independent review is genuinely unavailable, the ticket says so in its
`### Tier` section, in those words. It does not silently drop to standard.

## Rationale

Independence here means *not sharing the reasoning that produced the work*,
not *being a different kind of entity*. A reviewer that has not seen why the
executor thought the change was correct will check whether it is correct.

This catches the specific failure the policy is built around: an
implementation satisfying the letter of every acceptance criterion while
missing the intent, accompanied by a fluent summary explaining why it is fine.
A reviewer reading only the ticket and the diff is not exposed to that summary.

What it does not provide is accountability, and the decision does not pretend
otherwise. The independence is real; the judgement remains the maintainer's,
and so does responsibility for anything published here.

## Consequences

- **Positive:** the separation-of-duties rule stays enforceable at this scale
  instead of becoming an aspiration.
- **Positive:** the failure mode the review exists to catch is the one AI
  review is genuinely good at — verifying a claim against an artifact.
- **Negative:** independent review is weaker than a second human on questions
  of judgement, taste, and whether the work was worth doing at all.
- **Negative:** it can be defeated by an executor who writes acceptance
  criteria loose enough to pass. The ticket, not the review, is the real
  control.
- **Neutral:** unavailable review is recorded rather than worked around, so
  the gap is visible in the ticket history.

## Alternatives considered

### Alternative 1: Waive critical review for a single maintainer

Rejected. It removes the model's only enforcement, and it does so precisely
where a reader would look to see whether the model survives contact with
inconvenience.

### Alternative 2: Treat all work here as trivial or standard tier

Rejected. It is dishonest about the risk — a change to a policy document
published as evidence is not trivial — and it would require changing the
operative test, which is itself critical-tier work.

### Alternative 3: Require a human second reviewer

The correct answer with more than one maintainer. Rejected as unavailable
rather than wrong; the decision should be revisited if that changes.

## Migration

N/A. Applies from ADR-0001 forward.
