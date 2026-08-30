# Tier review model

Every ticket declares a risk tier. The tier sets the minimum review required
before merge.

The point of the model is that the tier is decided by **the semantics of the
change, not the location of the file it lands in**. "This file is important,
so be careful" is not a control; it is a mood. What follows is a test with a
yes/no answer.

---

## The operative test

Run it against your change. **Any one clause means `critical`:**

1. **Contract change.** You alter, remove, or change the meaning of an
   existing field, function signature, or return shape, such that an existing
   caller could observe the difference. *Adding a new optional field that
   defaults to a no-op is not this.*
2. **Behaviour change to an existing caller.** Existing code resolves
   differently with no new opt-in. *A new branch reached only by new callers
   is not this.*
3. **Ordering change.** You change the sequencing of an existing state
   machine or reducer. *Adding an observer hook that nothing existing reads is
   not this.*
4. **Determinism.** You touch the seeded random source, seed threading, or
   anything that could change a reproducible outcome.
5. **Process surface.** A schema migration, a CI configuration change, or a
   change to the review model itself.

If none hold, the tier is `standard`. In one line:

> **Could an existing caller, or a seeded run, notice this change without
> opting in? If yes, `critical`. If no, `standard`.**

---

## The tiers

| Tier | Typical work | Review | Gates |
|---|---|---|---|
| `trivial` | Documentation, comments, data additions, ticket edits | None; author self-merges | Mandatory |
| `standard` | Most feature work — new validators, resolvers, queries, components | None; author self-merges after a complete PR description with evidence per criterion | Mandatory |
| `critical` | Anything the operative test catches | One approval from **another agent**, human or AI, who must verify the evidence and run the suite themselves | Mandatory |

Gates are mandatory at every tier. There is no tier that skips the machine
checks — the tier governs *human and peer* review, not automated review.

---

## The scrutiny list, and why it is not a trigger

A handful of modules are where the operative test most often returns
`critical`: the central state object, the phase machine, the modifier
pipeline, the seeded random source, and the public action shapes.

Touching one of those is **a cue to run the test, not an automatic
escalation**. A purely additive extension that follows an established pattern
and changes no existing caller — a new optional field defaulting to null, a new
hook joining existing ones at a boundary, a new type nothing reads yet — stays
`standard`.

This distinction matters more than it looks. A model that escalates on file
paths trains contributors to treat escalation as noise, and an escalation
everyone ignores is worse than none.

---

## Separation of duties

The tier can move, but not freely, and not by the same party in both
directions:

- **The author proposes** the tier when writing the ticket.
- **The executor may raise** it — discovering mid-implementation that a change
  touches an existing contract — and records a one-line reason.
- **The executor may never lower it.**
- **Only the reviewer may lower** a tier the executor raised, and only as far
  as the operative test warrants, recording the reasoning.

The asymmetry is deliberate. A `critical` tier is what summons a second
reviewer, so an executor able to lower its own tier could dismiss its own
oversight. Raising is self-imposed cost and needs no check; lowering removes a
control and therefore cannot be done by the party the control is on.

This is the oldest idea in the document and the one that transfers furthest:
the party subject to a control does not get to remove it.

---

## Why "another agent, human or AI"

Critical review requires a second reviewer that is not the executor. It does
not require a human.

An independent agent, given the ticket and the diff but not the executor's
reasoning, catches a specific and common failure: an implementation that
satisfies the letter of every acceptance criterion while missing their intent.
The reviewer has to verify the evidence and run the suite itself rather than
accept the executor's summary — which is the whole value, since a persuasive
summary of wrong work is the characteristic AI failure mode.

What it does not substitute for is accountability. The independence is real;
the judgement is still mine.
