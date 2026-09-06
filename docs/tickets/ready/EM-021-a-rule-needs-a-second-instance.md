---
id: EM-021
title: A rule needs a second instance before it is written
status: ready
tier: critical
complexity: S
dependencies: []
---

# EM-021 — A rule needs a second instance before it is written

## Context

The five rule-bearing documents under `docs/` measured 3,152 words at
8b0a8b4 and 12,595 at 5d94db7, by `wc -w` over the five files at each
commit. Nearly all of the growth is rules, and nearly every rule the wave
EM-006 to EM-019-001 added came from one instance: one project's wave, one
ticket's review loop, one wrong figure. Each is read by every future
reviewer, on every round.

The cost of a rule written from one instance is visible at both ends. It is
a bet that the instance recurs, paid on every round whether it does or not.
And landing it is itself expensive: EM-019-001, a rule about how to write a
number, took three review rounds and six must-fixes, per its Review table —
a lot to spend preventing a two-word error that had happened once.

"Retiring a control" gives a rule a way out of these documents. Nothing
gives it a bar to clear on the way in. The contributor policy's §4 already
says what happens to a finding met once — it becomes a ticket, with
lineage — so the first instance is never lost. The question this ticket
answers is when a recorded instance becomes a rule.

## Specification

Documentation change only.

### Files

- `docs/tier-review-model.md`, "Retiring a control" — a paragraph before
  "Who this binds".

### Public surface

N/A — this repository publishes documents. The change adds a condition on
adding a rule and removes nothing.

### Behaviour

- A failure, a cost or a finding met once is recorded where it was met — in
  the ticket's Risks, or as a child ticket under §4 — and is not written
  into these documents as a rule until it is met a second time, in a second
  ticket or on a second project.
- The ticket that adds the rule names both instances in its Context.
- A rule that prevents an outcome that cannot be undone — third-party
  material published, the main branch force-pushed — may be written from
  one instance, and says so.
- The paragraph states the reason in the model's own terms — the brief is
  read on every round — and names its own instance count honestly: the
  wave that landed most of these rules would not have cleared this bar.
- Falsifier: retired when a failure recorded once and left unruled under
  this bar recurs at a cost greater than carrying the rule would have been,
  more than once over a stated population of closed tickets. The bar is
  then holding back rules that pay for themselves.

## What this refuses, and what it costs

**Refuses.** A rule from a single, clear, well-argued instance. Some of
those would have been right, and the second instance is the price of
finding out which.

**Costs.** The second instance costs whatever the failure costs to happen
again. For a wrong figure that is a correction; for a review loop that does
not converge, it is a day. The irreversible-outcome exception exists
because there is a class of failure whose second instance cannot be
afforded, and the paragraph names it so that the bar is not read as
absolute.

## Acceptance criteria

1. AC1: `docs/tier-review-model.md`, "Retiring a control", states the
   second-instance bar and where a first instance is recorded meanwhile.
2. AC2: The paragraph states the irreversible-outcome exception.
3. AC3: The paragraph names its own instance count.
4. AC4: The paragraph carries a **Retired when:** line.
5. AC5: Critical tier per ADR-0002: an independent agent that did not
   perform the work reviews this against the artifacts and records findings
   in two columns.

## Out of scope

- Retiring any rule the wave added from one instance. The bar applies from
  its landing forward; ADR-0001's rejection of backdating applies to
  un-landing.
- Defining what counts as "the same" failure across two instances. If two
  findings name the same rule and the same defect, they are two instances;
  a tighter definition is a later ticket with evidence.

## References

- `docs/tier-review-model.md`, "Retiring a control" — the section this
  paragraph joins, and "Who this binds", which it precedes.
- `docs/ai-contributor-policy.md` §4 — where a first instance already
  goes.
- EM-016 — which measured the brief's growth and made it navigable without
  bounding it; this ticket is the bound.
- EM-019-001 — the rule whose landing cost is the example.

## Notes

This ticket and EM-020 are raised together. EM-020 clears this bar with
five instances across four tickets; it is this rule's first test, landed
first so the test is real.

## PR Description

> Leave this section empty when authoring the ticket.
