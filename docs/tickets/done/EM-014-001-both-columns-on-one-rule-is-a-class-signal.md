---
id: EM-014-001
title: Both columns on one rule in consecutive rounds is a class signal
status: done
tier: critical
complexity: S
dependencies: [EM-007, EM-009, EM-010]
claimed_by: claude-fable-5-1
claimed_at: 2026-09-06
closed_at: 2026-09-06
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

### Ticket
EM-014-001 — Both columns on one rule in consecutive rounds is a class
signal

### Tier
`critical` — process-surface change (clause 5): it adds a stopping trigger
to the review and a field to the record.

**Independent review obtained**, per ADR-0002: a separate agent, given the
ticket, the diff and the two questions, and not the executor's reasoning,
reviewed the change in two rounds, read-only. Findings are under
Review; the tree was checked clean after each round.

### Summary
"What a review reports" gains one paragraph after the two-column rule: a
first-column finding on a rule followed in the next round by a
second-column finding on the same rule that lies inside the previous
round's fix sends the rule to redesign against its class, per the class
obligation; two findings not inside each other's fix do not fire it; the
distinction is read from two fields the record already carries; and the
signal is the single-rule complement of the repairs-of-repairs proportion
signal in "When review ends". The template's per-finding lines carry the
rule each finding landed on and whether it sits inside the previous fix.
The rule states its own falsifier, as the ticket's Behaviour does and as
ADR-0003's exemption clause asks this description to say.

### Acceptance criteria
- [x] AC1: the signal and the response — `docs/tier-review-model.md`,
  "What a review reports", the paragraph beginning "**Both columns on one
  rule in consecutive rounds is a class signal.**", "the next step is a
  redesign of the rule against its class".
- [x] AC2: the distinction from two unrelated adjustments by the
  inside-the-previous-fix field, adding no new judgement — same paragraph.
- [x] AC3: how it differs from the repairs-of-repairs signal, single rule
  versus proportion of the round — same paragraph.
- [x] AC4: the per-round record carries the rule each finding landed on —
  `templates/PR-DESCRIPTION.md`, the per-finding lines, `<rule>`.
- [x] AC5: the cost beside the rule, findings exceeding must-fixes — same
  paragraph, with the 22-findings-to-1-must-fix figure and its source.
- [x] AC6: the ticket's own falsifier in its Behaviour section — present
  in the ticket as raised, and now stated with the rule as its Retired-when
  line.
- [x] AC7: independent review, in two columns — see Review.

### Falsification
N/A — no behavioural claim. What a reader does differently, per criterion:
- AC1: a reviewer who sees the pair names the signal instead of proposing a
  third adjustment, and the executor redesigns.
- AC2: a reviewer with two findings on one rule that are not inside each
  other's fix does not fire the signal.
- AC3: a reader knows which signal to look for when one rule oscillates in
  an otherwise productive round.
- AC4: a closing executor writes the rule name on every finding line, so
  the signal can be read later.
- AC5: an adopter knows the field costs one entry per finding, not per
  must-fix.

This wave's own records are the first test: every closed ticket's Review
section names the rule per finding from EM-009 onward, and no rule in the
wave drew opposite columns in consecutive rounds inside its own fix. The
closest case is EM-007's round 2, where the definition added for a round-1
note was itself the round-2 must-fix — same rule, same column both times,
which the signal correctly does not fire on.

### Out of scope (per ticket)
Confirmed: EM-007's cap, conditions and proportion signal are unchanged
(the paragraph references the proportion signal and does not edit it);
"the same rule" is not defined more tightly than by name.

### Review
| Round | Must-fix | Where (rules / lists / documents / tests) | Inside previous round's fix | Repaired by |
|---|---|---|---|---|
| 1 | 2 (of 9 findings) | documents: the paragraph said the record "already carries" a per-finding field this change adds, and priced one field where there are two (must-fix); placed so the two-column rule's evidence paragraph read as the signal's (must-fix); the figure's source by indirection; the signal against "Retiring a control"; "third adjustment" and a falsifier the record could not match; what the executor may do and what a redesign is for a prose rule; reading the record across a round boundary; the refusal unstated; "The record." paragraph listing per-round fields only | — | 45e9119 |
| 2 | 0 (of 1 note) | documents: the round-boundary sentence read as a duty to commit per round | 1 of 1 | the closing commit |

Derived total: 2 must-fix over two rounds.
Round 1 by column and rule — permits: R1.1, this rule's cost and its
description of the record (remedy: "carries", two fields, the field on both
template lines; a tightening whose cost is one yes/no on every first-column
finding, 14 across the five closed critical records at 50fa1d5 by the
reviewer's count); R1.2, placement (remedy: after "A tightening states its
cost"); R1.3, the figure's source (remedy: c0111ae's round-1 review, in
3da6c57); R1.4, precedence against "Retiring a control" (remedy: one
clause). Refuses: R1.5, "third adjustment" and the falsifier's readability
(remedy: "a further adjustment"; the reviewer records the adjustment it
would have proposed); R1.6, the executor's options and the redesign's form
(remedy: §6's form; repair of the instance permitted and tested next
round); R1.7, the record across a round boundary (remedy: the brief or the
ticket); R1.8, the refusal (remedy: stated); R1.9, "The record." paragraph
in "When review ends" lists per-round fields only — recorded, outside
Files, for whichever ticket next touches that paragraph. Round 2's one
note was inside R1.7's remedy and is taken at close: "may commit".

**Departure from Behaviour, recorded.** The ticket's Behaviour bullet 2
says the distinction "is read from two fields the record already carries
— the column, and whether the finding sits inside the previous fix". Its
Files says the record "gains one field: the rule each finding landed on".
At 50fa1d5 the record carried inside-previous-fix per round, as `m of n`,
not per finding; the two sentences could not both be true of it. The
landed text says the record "carries for every finding" both fields, and
the cost is two fields per finding, not one; the ticket's Costs section,
which priced one, is superseded by this description. The correction was
directed by a review must-fix, confined to the description of the record,
and leaves the signal's conditions as the ticket states them.
Post-review tree check after each round: `git status --porcelain` empty,
`git worktree list` showing only the main tree.

### How to verify
1. `grep -n "Both columns on one rule" docs/tier-review-model.md` — one
   paragraph, inside "What a review reports", after the two-column rule.
2. `grep -n "<rule>" templates/PR-DESCRIPTION.md` — the field on both
   finding lines.
3. `wc -w` at the baseline and at close: tier model 3,537 to 3,993 and template 799 to 837, as the reviewer measured at 50fa1d5 and 45e9119.

### Risks / follow-ups
- The field requires every rule to be nameable, which is EM-014's
  obligation; a finding against prose that is not a rule is named by its
  section, as this wave's records have done.
- The signal's falsifier needs three redesigns to test; this repository has
  produced none yet.

