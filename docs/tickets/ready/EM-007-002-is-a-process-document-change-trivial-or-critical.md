---
id: EM-007-002
title: A change to a process document is trivial by the operative test and critical by ADR-0002
status: ready
tier: critical
complexity: S
dependencies: []
---

# EM-007-002 — Is a change to a process document trivial or critical?

## Context

Raised by the independent review of EM-007 (round 2, finding 12) and again
by the review of EM-012-001 (round 2, finding R2.2). Two published
statements give different answers for the same change.

ADR-0002's Context: "Changes to process documents are process-surface
changes, which the operative test classifies as critical. So this is not a
rare case: on a repository whose content *is* process documentation, most
substantive work is critical tier."

`docs/tier-review-model.md`, "The operative test", as EM-012-001 leaves it:
a change is `trivial` where "nothing a program executes and nothing a
caller reads as a contract is touched", and the tier table's `trivial` row
names documentation and ticket edits. A process document is read by
contributors, not by programs.

So a one-word fix to `docs/ticket-lifecycle.md` is `critical` by the
decision record and `trivial` by the model. Four tickets closed here on the
narrow reading — that ADR-0002 governs changes altering a rule or a
procedure, and not other documentation edits — and each recorded that
reading in its own Notes: EM-007-001, EM-010-002, EM-012-001-001, and the
entries of the batch EM-017. The reading is nowhere in the model or the
record it interprets.

## Specification

This ticket carries a question the contributor policy's §3 reserves to the
maintainer. It is not ambiguous — both readings are coherent — and it is
not the executor's to answer, because it resolves a conflict between a
decision record and the model that record governs, and because one of the
two available answers removes a control from the party the control is on.

The answers available, with what each costs:

1. **ADR-0002 governs as written.** Every change to a process document is
   `critical` and summons an independent reviewer. Cost: a typo fix in the
   lifecycle costs a review round; the batching path EM-012 added becomes
   unusable on this repository, because nothing here would ever be
   `trivial`; the four tickets closed on the narrow reading were closed at
   the wrong tier, and the record should say so.
2. **The narrow reading governs, and is written down.** A change to a
   process document is `critical` when it adds, alters or retires a rule or
   a procedure, and `trivial` when it does not. Cost: the line between
   "alters a rule" and "does not" is drawn by the executor, at the moment
   the executor would like the answer to be `trivial` — which is the
   failure ADR-0001's Alternative 3 rejected in a different form. The
   mitigation is that the executor may never lower a tier, only raise it.
3. **Something else**, including amending ADR-0002 under the
   amendment-with-record path, which is itself `critical` work.

What the executor needs in order to proceed: the maintainer's choice among
those, or a different one. The implementer then writes it into
`docs/tier-review-model.md` where the operative test states the `trivial`
line, records the decision per `docs/adr-process.md` since it is a workflow
rule changing, and — under answer 1 — corrects the record of the four
tickets closed at `trivial`.

## Acceptance criteria

1. AC1: `docs/tier-review-model.md` states, in one or two sentences, when a
   change to a process document is `critical` and when it is `trivial`.
2. AC2: The statement and ADR-0002 agree, or ADR-0002 is amended with a
   record per "Retiring a control".
3. AC3: The rule carries a **Retired when:** line.
4. AC4: Every ticket already closed at a tier the decision contradicts is
   named in the pull-request description, with what the record does about
   it.
5. AC5: Critical tier per ADR-0002: an independent agent reviews this
   against the artifacts and records findings in two columns.

## Out of scope

- Any change to the operative test's five clauses.
- Any change to what each tier requires. This ticket decides which tier a
  class of change is, not what that tier costs.

## References

- ADR-0002, Context — the sentence one reading follows.
- `docs/tier-review-model.md`, "The operative test" and "The tiers".
- ADR-0001, Alternative 3 — "'substantive' is decided by the person who
  wants the exemption, and the exemption widens", which is the hazard in
  answer 2.
- EM-007-001, EM-010-002, EM-012-001-001, EM-017 — closed on the narrow
  reading.

## Notes

The question is small and its answer is load-bearing: it decides whether
this repository's own work is reviewable at the cost it has been paying, or
at several times that cost.

## PR Description

> Leave this section empty when authoring the ticket.
