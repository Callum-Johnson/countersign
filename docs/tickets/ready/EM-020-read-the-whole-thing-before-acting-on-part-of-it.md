---
id: EM-020
title: Read the whole thing before acting on part of it
status: ready
tier: critical
complexity: S
dependencies: []
---

# EM-020 — Read the whole thing before acting on part of it

## Context

Measured on this repository's closed records at 5d94db7. The Review tables
of the closed tickets record 33 must-fixes over 29 review rounds, by

```sh
grep -h "^| [0-9] | " docs/tickets/done/EM-0*.md \
  | awk -F'|' '{r++; gsub(/ *\(.*/,"",$3); m+=$3} END {print r, m}'
```

Of those, the rounds after a first round that found any must-fix are listed
by

```sh
grep -h "^| [0-9] | " docs/tickets/done/EM-0*.md | awk -F'|' '$2+0>1 && $3+0>0'
```

which prints four rows — EM-007 round 2, EM-011 round 2, EM-016 round 2,
EM-019-001 round 2 — whose must-fix cells sum to 5, and whose
inside-previous-fix cells say that every one of those five sat inside the
previous round's own repair. So 28 must-fixes were found in first rounds
and 5 afterwards, and all 5 were damage done by repairing the round before.

Each repair was right where it pointed and wrong beside it. An exemption
clause was added under a trigger and swallowed it, because a newly added
document has no row by definition (EM-016). A date was placed outside a rule
whose neighbouring bullet names a date as a baseline (EM-019-001). A source
was attributed to the wrong project, and the repair of that attribution
attributed it to the wrong project again one sentence earlier (EM-011). The
reviewer reads the section fresh each round; the executor had read one
sentence.

The same failure sits one step earlier. Two tickets contradicted themselves
— EM-007's Behaviour against its own Context, EM-014-001's Files against
its own Behaviour — and each was transcribed faithfully and cost a must-fix.
The executor had read the ticket in parts.

And a third form, mechanical. Repairs that re-flowed text produced ragged
paragraphs and over-long lines that the next round flagged; the words
"ragged", "re-flow", "long line" and "orphan line" appear 22 times in the
closed records, by `grep -hoiE` over `docs/tickets/done/` at 5d94db7. No
document states a wrap convention. The initial commit arrived wrapped at 80
columns — the longest line of the policy at 38a7e61 is 80 characters, by
`awk '{print length($0)}' | sort -n | tail -1` — and every edit since has
matched the surrounding text, which is how a convention nobody chose came
to generate findings.

## Specification

Documentation changes only. One rule, stated once, applied at two moments.

### Files

- `docs/tier-review-model.md`, "When review ends" — a paragraph after
  "Repairs of repairs", where the evidence for the rule is.
- `docs/ai-contributor-policy.md` §7 — checklist item 2 extended, referring
  to the paragraph above.

### Public surface

N/A — this repository publishes documents. The change adds a discipline to
the executor's sequence and removes a class of finding from the reviewer's.

### Behaviour

- Before a repaired change goes to the next round, the executor reads the
  whole section as it now stands, as the reviewer will, and not the lines
  the repair touched.
- At claim, the executor reads the ticket whole and checks that its
  Context, Files and Behaviour agree with one another; where they do not,
  it blocks under §3 before writing anything. Checklist item 2 says so and
  names the paragraph in the tier model as the same reading.
- A repair does not re-flow text it did not change. These documents are
  not wrapped by rule, and a difference in wrapping between paragraphs is
  not a finding.
- The rule carries the five-of-five figure with its baseline, and its
  falsifier: retired when, over a stated population of critical-tier
  tickets closed under this rule, must-fixes found after the first round sit
  inside the previous round's repair as often as they did before it — which
  at 5d94db7 was every one.

## What this refuses, and what it costs

**Refuses.** A repair handed back on the strength of the lines it touched.
And, at claim, a ticket that disagrees with itself: the executor may no
longer choose the reading it prefers and proceed, which is what §3 already
said and what two tickets here did anyway.

**Costs.** One full read of a section per repair and one full read of a
ticket per claim. On this repository's 29 rounds that is 29 section reads
at most, against the 5 rounds the reads would have removed — which is not a
saving in reads, it is a saving in rounds, and a round is the expensive
unit. The re-flow clause costs nothing and removes 22 mentions' worth of
finding traffic.

## Acceptance criteria

1. AC1: `docs/tier-review-model.md`, "When review ends", states the
   whole-section read before a repair is handed back.
2. AC2: `docs/ai-contributor-policy.md` §7 item 2 requires the ticket's
   Context, Files and Behaviour to agree, names §3 as where a disagreement
   goes, and refers to the tier model's paragraph as the same reading.
3. AC3: The rule is stated once, in the tier model, with its falsifier; the
   checklist item references it and restates nothing.
4. AC4: The falsifier names its baseline figure and the commit it was
   measured at.
5. AC5: The tier model states that a repair does not re-flow what it did
   not change and that wrapping is not a finding.
6. AC6: Critical tier per ADR-0002: an independent agent that did not
   perform the work reviews this against the artifacts and records findings
   in two columns.

## Out of scope

- Any change to what a review reports or when it ends.
- Re-flowing or un-wrapping any existing text. A whole-repository re-flow
  is a change on every line of blame for no rendered difference.
- Any machine check for line length, links or figures. The maintainer has
  declined machine gates for this repository.

## References

- `docs/tier-review-model.md`, "When review ends" — the loop this rule
  shortens, and its own evidence that repairs of repairs are the loop's
  steady state.
- `docs/ai-contributor-policy.md` §3 and §7 — where a self-contradicting
  ticket goes, and the checklist that will ask.
- EM-007, EM-011, EM-016, EM-019-001 — the four closed records whose second
  rounds are the evidence.

## Notes

Five instances across four tickets, which clears the bar EM-021 proposes
for a new rule. The two tickets are raised together because this one is
the second's first test.

## PR Description

> Leave this section empty when authoring the ticket.
