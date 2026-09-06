---
id: EM-011
title: Review runs in its own worktree, and the tree under review is checked afterwards
status: in-progress
tier: critical
complexity: S
dependencies: []
claimed_by: claude-fable-5-1
claimed_at: 2026-09-06
---

# EM-011 — The reviewer does not touch the tree

## Context

EM-006 adds to the identical-script rule the constraint that a gate script must
not mutate state outside the working tree, with the editable-install example:
one agent's gate run repointing every parallel worktree's imports. This ticket
is the same rule one level up. A review must not mutate the tree it reviews.

The falsification gate asks a reviewer to do something that looks like
mutation: apply a wrong implementation, run the suite, count. The gate is
right to ask it. The question is where, and the answer has to be a worktree
the reviewer owns, because the alternative was demonstrated on the
control-plane project that implements this process mechanically.

On OMN-021 there, one reviewer left a `sitecustomize.py` at the root of the
tree under review. The file is recorded in the project's own policy module as
the file round 12's reviewer left in the working tree, and it is what the
lint gate failed on. The mechanism, stated so it can be reproduced rather
than as an incident: the interpreter imports a module of that name at
start-up from any directory on its path, so a copy that calls `os._exit(0)`
under the test runner and the type checker makes both gates exit zero having
examined nothing, and only a gate that reads the file as text — lint — sees
it. Another reviewer on the same ticket left a registered worktree, which the
main tree's status command does not show. Both were found by the executor,
and the executor's answer was to check the tree's status and the worktree
list before every gate run, by hand, as a private discipline. That is a rule
that should be written down, and it belongs to the review, not to the
executor.

The point is not that a reviewer was careless. It is that a review process
which can leave anything in the tree has changed what the next round reviews,
and the record can no longer say whether a finding was in the work or in the
review of it.

## Specification

Documentation changes only.

### Files

- `docs/quality-gates.md` — the identical-script rule section as EM-006 lands
  it, or a new section "Review isolation" beside it.
- `docs/tier-review-model.md` — the reviewer section gains one sentence
  stating where the reviewer works and referencing the gates document for the
  rule.

### Public surface

N/A — this repository publishes documents. The change adds a constraint on
how review is conducted and changes nothing about what it examines.

### Behaviour

- The rule states that review, including any mutation the falsification gate
  asks for, runs in a worktree the reviewer creates, owns and removes. The
  tree under review is read, never written, by the reviewer.
- The rule states that the tree under review is checked after the review
  returns, before any repair or further round: the status command reports
  nothing untracked and nothing modified, and the worktree list shows nothing
  the executor did not register. Anything found is a finding against the
  review, recorded as such, and is removed before the tree is used again.
- The rule gives the `sitecustomize` mechanism as its example in engineering
  terms — a start-up import, a zero exit, two gates that examined nothing —
  so that a reader understands the class and not only the file.
- The rule states why this is the executor's check and not the reviewer's
  promise: the party that will be blamed for a finding is the party that must
  be able to show the tree was its own.

## What this refuses, and what it costs

> Added 2026-09-05 on review of the wave, applying EM-010's two questions to the ticket that proposes them. A figure measured here names its baseline in the same sentence; a figure from a private project names the ticket section it is taken from; an assumption says so. Raised alongside EM-014; corrected after independent review of c0111ae.

**Refuses.**

- Review that writes to the tree under review, in any form — which includes
  any reviewer tool that runs the suite or applies a mutant in place, and an
  agent handed a path with no ability to create a worktree. A read-only
  hosted review writes nothing and is not refused by this rule; what it
  cannot do is discharge the run-the-suite duty, and that refusal is the tier
  model's, not this ticket's.
- Review on a checkout where a worktree cannot be created, or where creating
  one costs a full environment build. The rule has no fallback for either.

**Costs.**

- Per review: create a worktree, build its environment, run, remove. Under
  EM-006's no-global-mutation constraint each worktree needs its own
  interpreter environment, so this is minutes and disk per review round, not
  seconds. On OMN-021's fourteen rounds, per the per-round counts EM-007's
  Context quotes, that is fourteen environments if each round builds afresh —
  which the rule implies and the record does not state.
- Per round: the executor's status-and-worktree-list check before the next
  gate run. Seconds, but one more step in the sequence, and the executor's
  step — the ticket is right that it must be, and that is still a cost the
  executor pays for the reviewer's discipline.

## Acceptance criteria

1. AC1: `docs/quality-gates.md` states that review runs in the reviewer's own
   worktree and that the tree under review is not written by the reviewer.
2. AC2: The document names the post-review check — status clean, worktree
   list as the executor left it — and states that anything found is a finding
   against the review.
3. AC3: The `sitecustomize` mechanism is given as the example, in engineering
   terms, with the class it belongs to stated.
4. AC4: `docs/tier-review-model.md`'s reviewer section states where the
   reviewer works in one sentence and references the gates document.
5. AC5: Critical tier per ADR-0002: an independent agent that did not perform
   the work reviews this against the artifacts and records findings in the
   pull-request description.

## Out of scope

- Mechanising the check. A project that dispatches reviewers can make the
  post-review check a gate; that is the project's ticket, not this one.
- Any change to what the reviewer receives or does. The falsification gate's
  mutation-and-count is unchanged; only its location is constrained.

## References

- EM-006 — the no-global-mutation constraint this ticket extends to review.
- `docs/quality-gates.md`, the identical-script rule — the section this
  ticket sits beside.
- `docs/tier-review-model.md` — the reviewer section this ticket amends.
- OMN-021 on the control-plane project — the policy module's comment that
  records the file, and its commits for rounds 12 and 13.

## Notes

**On the mechanism's exact reach.** The source project's own record, in the
same comment, corrects an earlier claim about exactly when the interpreter
reaches a root-level `sitecustomize`, and the correction is that it depends on
the invocation. The example here is stated at the level that does not depend
on it: a start-up import that exits zero neutralises whichever gates reach
it, and the lint gate is the one that reads files rather than running them.
An implementer quoting a more precise mechanism should quote the source
project's comment rather than this ticket.

**Working this with EM-007 to EM-010.** See EM-007's Notes.

## PR Description

> Leave this section empty when authoring the ticket.
