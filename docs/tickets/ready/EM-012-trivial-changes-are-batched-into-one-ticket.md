---
id: EM-012
title: Trivial changes are batched into one ticket
status: ready
tier: critical
complexity: S
dependencies: []
---

# EM-012 — Trivial changes are batched into one ticket

## Context

`docs/tier-review-model.md` scales review to risk. It scales nothing else. A
`trivial` change and a `critical` one pay the same ticket file, the same
claim and close commits, the same pull-request description and the same gate
run, because `docs/ticket-lifecycle.md` describes one lifecycle and
`docs/quality-gates.md` makes the gates mandatory at every tier.

The measured instance is on the control-plane project that implements this
process mechanically. Adding one line to `.gitignore` — an editor's state
directory, joining two entries already there — cost six commits, two moves
through the ticket directories, a pull-request description, and a full gate
run of about twelve minutes, because the gate script runs the whole suite
regardless of what the diff touches. The tier was correctly `trivial`
throughout. Nothing was done wrong; the cost is what the documented process
charges for its smallest unit of work.

The failure this produces is not slowness. It is that a process too expensive
for a one-line change gets bypassed for one-line changes, and the model
already names that hazard in its own words: an escalation everyone ignores is
worse than none. A lifecycle whose cheapest path is twelve minutes and six
commits trains contributors to commit small things without it.

## Specification

Documentation changes only.

### Files

- `docs/ticket-lifecycle.md` — a new section, "Batching trivial work", after
  "Claiming".
- `docs/tier-review-model.md` — one sentence in the tier table's `trivial`
  row or beneath it, pointing at the lifecycle section.

### Public surface

N/A — this repository publishes documents. The change adds a path through
the lifecycle and removes none.

### Behaviour

- A change whose operative test returns `trivial` may be committed against an
  **open batch ticket** rather than a ticket of its own. Every other tier
  keeps its own ticket.
- The batch ticket is an ordinary ticket in every other respect: a flat
  identifier, claimed by the documented procedure, held by one agent, living
  in the active state while held, closed and merged like any other. It is not
  a standing ticket that never closes — a ticket permanently in `active/`
  makes the board describe work nobody is doing.
- **Each entry is listed individually** in the ticket, with what changed, the
  operative test's answer for that entry, and its evidence. The batch is a
  container for separately justified changes, not one change with several
  parts.
- A change that turns out to return `standard` or `critical` **leaves the
  batch** and takes its own ticket. Discovering that after it was committed
  to the batch is recorded in the batch ticket as a finding, not quietly
  moved.
- The batch closes on a stated cap — a number of entries or an age, whichever
  comes first — so it cannot accumulate indefinitely, and so the gate run at
  its head stays attributable to a diff small enough to read.
- Gates run once, on the batch's head, under the existing rule. That is where
  the saving is: one run for several entries rather than one run each.
- **Only the holder commits to the batch.** An agent wanting a trivial change
  while another holds the batch opens the next one rather than appending. A
  shared append-only ticket file conflicts between agents, and the file move
  is the crude lock this lifecycle already relies on.

## What this refuses, and what it costs

> Added 2026-09-05 on review of the wave, applying EM-010's two questions to the ticket that proposes them. Every figure names its baseline in the same sentence. Raised alongside EM-014.

This is the only ticket in the wave whose primary effect is in EM-010's second
column: it adds a cheaper path and refuses nothing that was previously
allowed. That is worth saying plainly, because the other six are all
first-column tickets, and a wave of seven whose one loosening is a batching
path for trivial work has not answered the second question for standard-tier
work, which is where most of the wave's cost lands.

**Refuses.**

- Appending to a batch another agent holds; the next agent opens the next
  batch. A standing batch is refused by the cap.
- Silent reclassification. A change found to be above trivial leaves the
  batch with a recorded finding, not a quiet move.

**Costs.**

- Per entry: the operative test's answer and its evidence, written
  individually. The saving is one gate run per batch rather than one per
  entry, and the Notes already state that the first entry saves nothing.
- The scrutiny cost is the real one and the Notes state it: the batch is the
  least-read path in the lifecycle. Measure it the only way it can be
  measured — count reclassifications out of batches over the first ten
  batches, and if the count is zero, ask whether nobody is reading them.

## Acceptance criteria

1. AC1: `docs/ticket-lifecycle.md` describes the batch ticket: what may join
   it, that entries are listed individually with their own operative-test
   answers, and that it is claimed, closed and merged as an ordinary ticket.
2. AC2: The section states the cap that closes a batch, as a named default
   with its reasoning.
3. AC3: The section states that a change reclassified above `trivial` leaves
   the batch, and that the reclassification is recorded rather than tidied.
4. AC4: The section states the single-holder rule and why, referencing the
   claiming lock it depends on.
5. AC5: `docs/tier-review-model.md` points at the section from the `trivial`
   row without restating the rule.
6. AC6: The section states what batching does **not** save — see Notes — so
   that a reader does not adopt it expecting a cheaper first change.
7. AC7: Critical tier per ADR-0002: an independent agent that did not perform
   the work reviews this against the artifacts and records findings in the
   pull-request description.

## Out of scope

- **Scoping the gates to what the diff touches.** That is the other lever on
  the same cost, and the only one that lowers the floor for a change with no
  siblings to batch with. It is a change to `docs/quality-gates.md`'s
  identical-script rule and is not decided here.
- Any change to the operative test, or to what `trivial` means. This ticket
  changes how trivial work is tracked, never what qualifies.
- Batching `standard` work. The saving is smaller and the risk of hiding a
  contract change among several is real; if wanted, it is its own ticket with
  its own argument.

## References

- `docs/ticket-lifecycle.md` — "Claiming", whose file-move lock the
  single-holder rule depends on.
- `docs/tier-review-model.md` — the tier table, and its reasoning that an
  escalation everyone ignores is worse than none.
- `docs/quality-gates.md` — gates mandatory at every tier, which is the
  dominant cost being amortised.
- OMN-025 on the control-plane project — the measured one-line change, whose
  pull-request description records the six commits and the gate run.

## Notes

**What this does not save, stated plainly because AC6 requires the document
to say it.** Batching amortises; it does not reduce. The first trivial change
in a batch costs exactly what a solo trivial ticket costs, and the measured
instance above had no siblings to batch with — this rule would not have made
that change faster. The saving appears only across several, and a project
with few trivial changes should expect little from it. The lever that lowers
the floor for a lone change is gate scoping, which is deliberately left open
above.

**The risk, and why the mitigation is not a guarantee.** A batch is a
plausible place to hide a change that is not trivial, precisely because it is
a list of things nobody expects to read closely. Listing each entry with its
own operative-test answer makes hiding one a false statement a reviewer can
check rather than an omission nobody can see. That is a mitigation. It is not
a guarantee, and a project adopting this accepts that the batch is the least
scrutinised path it has.

**Working this with EM-007 to EM-011.** Those five came from one review loop
that did not stop. This one came from the opposite end of the same
question — process cost that does not scale down — and was raised after the
maintainer observed that a one-line change had cost more than it was worth.
None of the five bounds effort to the size of a change; this one does.

## PR Description

> Leave this section empty when authoring the ticket.
