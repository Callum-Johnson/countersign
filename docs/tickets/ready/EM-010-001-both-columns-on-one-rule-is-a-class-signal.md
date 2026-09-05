---
id: EM-010-001
title: Both columns landing on one rule in consecutive rounds is a class signal
status: ready
tier: critical
complexity: S
dependencies: [EM-010, EM-009]
---

# EM-010-001 — Both columns on one rule is a class signal

## Context

Raised while working EM-010's *refuses and costs* section, and moved here on
independent review of c0111ae, which found it placed as a "proposed addition"
outside any ticket's Specification and without a stated cost.

EM-010's two columns have a failure mode the ticket does not name. Round one
finds, in column 1, that a rule lets something through, and tightens it.
Round two finds, in column 2, that the tightening refuses honest work, and
loosens it. Round three tightens it again. Each finding is correct on its own
terms, each is a must-fix of equal rank, and the loop never disagrees with
itself. EM-007's cap ends it after three rounds. Nothing ends it in round
two, when the shape is already visible.

EM-009 already has the concept that fits: a finding that keeps landing in the
same place is one instance of a class, and the repair is at the class. A rule
that both columns land on in consecutive rounds is a rule whose current form
cannot be adjusted into acceptability, and the next step is to redesign it,
not to adjust it a third time.

## Specification

Documentation changes only.

### Files

- `docs/tier-review-model.md` — one paragraph in the section EM-010
  introduces, after the two-column rule.
- `templates/PR-DESCRIPTION.md` — the per-round record EM-007 introduces
  gains one field: the rule each finding landed on.

### Public surface

N/A — this repository publishes documents. The change adds a stopping
trigger to the review and a field to the record.

### Behaviour

- When a column-1 finding and a column-2 finding land on the same rule in
  consecutive rounds, the next step is a redesign of the rule against its
  class, per EM-009, and not a third adjustment. The reviewer names the
  signal; the executor does the redesign.
- The per-round record carries, for each finding, the rule it landed on, so
  that the signal can be read from the record rather than remembered.
- The trigger is stated as a class signal, not as a cap. A rule may be
  adjusted twice for two unrelated reasons; the signal is two findings from
  opposite columns on the same rule in adjacent rounds.

## What this refuses, and what it costs

**Refuses.** A third adjustment that would have been right. Some rules do
converge on the third try; this trigger sends them to redesign instead. The
cost of a wrong redesign is a round; the cost of a fourth adjustment on a
rule that will not converge is EM-007's cap.

**Costs.** One field per finding in the per-round record — the rule name.
On OMN-021's 46 must-fixes, per its Review section as EM-007's Context quotes
it, that is 46 short entries across fourteen rounds. Nothing else.

## Acceptance criteria

1. AC1: `docs/tier-review-model.md` states the trigger — opposite columns,
   same rule, consecutive rounds — and that the response is redesign per
   EM-009.
2. AC2: The statement distinguishes the signal from two unrelated
   adjustments to one rule.
3. AC3: `templates/PR-DESCRIPTION.md`'s per-round record carries the rule
   each finding landed on.
4. AC4: The cost — one field per finding — is stated beside the rule.
5. AC5: Critical tier per ADR-0002: an independent agent that did not
   perform the work reviews this against the artifacts and records findings
   in the pull-request description, in EM-010's two columns.

## Out of scope

- Changing EM-007's cap or conditions. This trigger fires before the cap;
  the cap is unchanged.
- Defining "the same rule" more tightly than by name. If two findings name
  the same rule, they are on the same rule.

## References

- EM-010 — the two columns this trigger reads.
- EM-009 — the class obligation the response invokes.
- EM-007 — the per-round record the new field joins, and the cap this
  trigger precedes.

## Notes

**Its own falsifier, per EM-014.** Retired when three rules sent to redesign
by this trigger would each have converged on the third adjustment — shown by
the redesign reproducing what the third adjustment would have been.

## PR Description

> Leave this section empty when authoring the ticket.
