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

---

## When review ends

A review usually ends when a round returns clean. Where a round cannot return
clean, a rule is needed, because without one "every round found something"
reads as the review earning its keep — and under this model's own reasoning
it is the opposite. A process with no statement of what a converged review
looks like cannot be shown to have converged, only to have been stopped. The
falsification gate asks a test to name what would make it fail; the same is
asked here of the review.

One class of change guarantees a round that cannot return clean: an
enumeration maintained against an adversary — a list of paths, names or
shapes that a control must catch. A reviewer briefed to find the entry the
list is missing will find one every round, because the list is finite and the
adversary's options are not.

A round is one reviewer's pass over one commit, and the repair it produces.
A must-fix is a finding the reviewer records as blocking merge; the report
that records it is described in the previous section. A round ends the loop
**without a further fix** under any of three conditions. Each names where its
findings go.

1. **The round finds no must-fix.** Review is complete.
2. **Every must-fix in the round lies inside a limit the ticket already
   records** — an out-of-scope item, a stated narrowing, a child ticket. The
   reviewer's record says which limit each finding sits inside; the executor
   routes the finding but does not reclassify it, since the party subject to
   a control does not get to remove it. The findings go to the ticket that
   owns the limit, raised if it does not exist. Review of this ticket is
   complete, with the limit and the findings routed to it stated in the
   pull-request description as they are, not softened.
3. **Every must-fix in the round adds an entry to an enumeration the change
   maintains against an adversary.** The entries are added once; the list is
   recorded as best-effort with the review's coverage stated; and further
   rounds against the list are list-building, not review. A finding that
   adds an entry to a list is evidence the list is a list, not evidence the
   rules it serves are wrong, and it does not reopen review of those rules.

**The cap.** A ticket takes at most **three** review rounds before it blocks
to the maintainer with its review record attached. Three is a default, named
as one, and the reasoning is one ticket's record: on OMN-021, the control-plane
ticket this section was measured on, the per-round must-fix counts in its
Review section run 7, 5, 2, 3, 4, 2, 2, 2, 6, 5, 3, 1, 2, 2 over fourteen
rounds, the eight rules it built were unchanged after round 6, and every
finding from round 7 onward was in two path lists. Rounds 1 to 3 found the
rules' original defects; rounds 4 to 6 repaired the repairs, which is the
signal below; everything from round 7 was lists. Three is set at the point
where original rule defects stopped, and the record supports no stronger
claim for it than that. Blocking at the cap is a success path in exactly the
sense of the contributor policy's §3: the executor has correctly identified
that the loop is not converging, and the alternative is another round that
looks like progress. The record travels with the block: the per-round table
is appended to the ticket file under the `BLOCKER:` comment, since the
pull-request description it would otherwise live in is not written until
close.

The cap is not the rule; the conditions are. A cap alone ends a review that
is still finding rule defects, which is the wrong review to end. The
conditions end the review that cannot converge, and the cap catches the case
where nobody applied them.

**Repairs of repairs.** When a round's must-fixes are mostly inside the
previous round's fix, the next step is not another per-finding repair but a
redesign of the fix against its class — the class obligation EM-009 adds to
the falsification gate, referenced here and not restated. On OMN-021, 29 of
the 46 must-fixes, derived from the per-round figures in its Review section,
were defects in a fix rather than in the original work.

**The record.** The pull-request description's Review section carries, per
round: the round number, the must-fix count, where the findings sat (rules,
lists, documents, tests), how many sat inside the previous round's fix, and
the commit that repaired it. **The total is derived from the rows and never
asserted beside them.** OMN-021's own total drifted three times — its Review
section records "sixteen", "thirty-five" and "twenty-nine" — while it was
asserted rather than derived.
