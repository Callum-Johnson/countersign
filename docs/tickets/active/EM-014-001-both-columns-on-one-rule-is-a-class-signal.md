---
id: EM-014-001
title: Both columns on one rule in consecutive rounds is a class signal
status: in-progress
tier: critical
complexity: S
dependencies: [EM-007, EM-009, EM-010]
claimed_by: claude-fable-5-1
claimed_at: 2026-09-06
---

# EM-014-001 — Both columns on one rule in consecutive rounds is a class signal

## Context

Raised from the independent review of c0111ae, the commit that raised EM-014
and added the *refuses and costs* sections to the wave. That review's finding
11 found a stopping trigger proposed inside EM-010's section, outside any
Specification and without a cost. Lineage records where a ticket came from:
this one came from EM-014's review. The gap it addresses is in EM-010's
design, which is why EM-010 is a dependency and not the parent.

EM-010's two columns have a failure mode the ticket does not name. Round one
finds, in column 1, that a rule lets something through, and tightens it.
Round two finds, in column 2, that the tightening refuses honest work, and
loosens it. Round three tightens it again. Each finding is correct on its own
terms, each is a must-fix of equal rank, and the loop never disagrees with
itself.

EM-007 already has a signal for repairs of repairs: when a round's must-fixes
are *mostly* inside the previous round's fix, redesign rather than repair.
That is a proportion of the round. It fires when ping-pong is most of what
the round found, and does not fire when one rule is ping-ponging inside a
round that is otherwise finding new things. This ticket adds the single-rule
form: one pair, opposite columns, adjacent rounds, same rule. EM-009 supplies
the response — a finding that keeps landing in the same place is one
instance of a class, and the repair is at the class.

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

- When a column-1 finding on a rule in one round is followed in the next
  round by a column-2 finding on the same rule **that lies inside the
  previous round's fix** — a field EM-007's record already carries — the
  next step is a redesign of the rule against its class, per EM-009, and not
  a third adjustment. The reviewer names the signal; the executor does the
  redesign.
- Two findings on one rule that are not inside each other's fix are two
  unrelated adjustments and do not fire the signal, whatever columns they
  fall in. The distinction is read from two fields the record already
  carries — the column, and whether the finding sits inside the previous
  fix — and adds no new judgement.
- The per-round record carries, for each finding, the rule it landed on, so
  that the signal can be read from the record rather than remembered.
- **Its own falsifier, per EM-014.** Retired when three rules sent to
  redesign by this signal each produced a redesign whose effect the
  per-round record shows to be the same as the third adjustment the reviewer
  had already proposed — that is, when the record shows the signal costing a
  round and buying nothing, three times.

## What this refuses, and what it costs

**Refuses.** A third adjustment that would have been right. Some rules do
converge on the third try; this signal sends them to redesign instead. The
cost of a wrong redesign is a round; the cost of a fourth adjustment on a
rule that will not converge is EM-007's cap.

**Costs.** One field per *finding* in the per-round record — the rule name.
Findings exceed must-fixes: round 1 of the review that raised this ticket
returned 22 findings and 1 must-fix. On OMN-021's 46 must-fixes, per its
Review section as EM-007's Context quotes it, 46 entries is therefore a
floor, not a total; the record does not give that ticket's finding count.
The field also requires every rule to be nameable, which is EM-014's
obligation, not this ticket's, and is why EM-014 is this ticket's parent.

## Acceptance criteria

1. AC1: `docs/tier-review-model.md` states the signal — column 1 then column
   2, same rule, adjacent rounds, the second inside the first's fix — and
   that the response is redesign per EM-009.
2. AC2: The statement distinguishes the signal from two unrelated
   adjustments to one rule by the inside-the-previous-fix field, and says
   the distinction adds no new judgement.
3. AC3: The statement says how this signal differs from EM-007's
   repairs-of-repairs signal: single rule versus proportion of the round.
4. AC4: `templates/PR-DESCRIPTION.md`'s per-round record carries the rule
   each finding landed on.
5. AC5: The cost — one field per finding, findings exceeding must-fixes — is
   stated beside the rule.
6. AC6: This ticket's own falsifier is stated in its Behaviour section.
7. AC7: Critical tier per ADR-0002: an independent agent that did not
   perform the work reviews this against the artifacts and records findings
   in the pull-request description, in EM-010's two columns.

## Out of scope

- Changing EM-007's cap, conditions, or proportion signal. This signal fires
  beside them; they are unchanged.
- Defining "the same rule" more tightly than by name. If two findings name
  the same rule, they are on the same rule.

## References

- EM-014 — the parent, whose review raised this; and whose falsifier
  obligation this ticket follows though it is exempt from it.
- EM-010 — the two columns this signal reads.
- EM-009 — the class obligation the response invokes.
- EM-007 — the per-round record the new field joins, its
  inside-the-previous-fix field which this signal reads, and its proportion
  signal which this one complements.

## Notes

**Working this with the wave.** Depends on EM-007 (the record), EM-009 (the
response) and EM-010 (the columns), and cannot land before all three. If the
wave is reviewed as one change, this ticket is reviewed with it.

## PR Description

> Leave this section empty when authoring the ticket.
