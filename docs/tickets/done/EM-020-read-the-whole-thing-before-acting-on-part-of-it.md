---
id: EM-020
title: Read the whole thing before acting on part of it
status: done
tier: critical
complexity: S
dependencies: []
claimed_by: claude-fable-5-1
claimed_at: 2026-09-06
closed_at: 2026-09-06
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
"ragged", "re-flow", "long line" and "orphan line", with their variants,
appear 22 times in the closed records at 5d94db7, by
`grep -hoiE "ragged|re-?flow|over-?long|long line|[0-9]+.character line|orphan line"`
over every file `git ls-tree` lists under `docs/tickets/done/` at that
commit. A different pattern gives a different count; the pattern is the
figure's baseline. No
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

### Ticket
EM-020 — Read the whole thing before acting on part of it

### Tier
`critical` — process-surface change (clause 5): it adds a discipline to
the executor's sequence in the review model and to the pre-flight checklist.

**Independent review obtained**, per ADR-0002: a separate agent, given the
ticket, the diff and the two questions, and not the executor's reasoning,
reviewed the change in two round(s), read-only. Findings are under
Review; the tree was checked clean after each round.

### Summary
"When review ends" gains one rule after "Repairs of repairs", with its
evidence and its falsifier: before a repair is handed back, the executor
reads the whole section as it now stands. The same reading is asked for at
claim by checklist item 2, which now requires the ticket's Context, Files
and Behaviour to agree and names §3 as where a disagreement goes. A repair
does not re-flow what it did not change, and wrapping is not a finding.
The index row for the section is updated in the same commit, per EM-016.

**The rule was applied to its own landing.** Before dispatching the review,
the executor read both edited sections whole and found two defects: the
claim-time check was stated in the model and in the checklist, so the rule
was in two places; and the index row for "When review ends" no longer
described the section. Both were fixed in a second commit before any
reviewer saw the change.

### Acceptance criteria
- [x] AC1: the whole-section read before a repair is handed back —
  `docs/tier-review-model.md`, "When review ends", the paragraph beginning
  "**The repair is read whole before it is handed back.**"
- [x] AC2: §7 item 2 requires Context, Files and Behaviour to agree, names
  §3, and refers to the model — `docs/ai-contributor-policy.md`, the
  checklist's second item.
- [x] AC3: stated once with its falsifier in the model; the checklist item
  references it — the model's sentence "The same reading is asked for at
  claim, by item 2 of the contributor policy's §7 checklist, which says what
  is checked and where a disagreement goes" points at the item and restates
  neither the check nor the destination.
- [x] AC4: the falsifier names five of five and 5d94db7.
- [x] AC5: a repair does not re-flow what it did not change; wrapping is
  not a finding — same paragraph, last two sentences.
- [x] AC6: independent review — see Review.

### The figures, each with its command
The row commands were run at afdbaa4 over `docs/tickets/done/`, before the
closing commit moves this ticket's own table there; the word counts are of
the content the closing commit carries, taken after its last edit to each
file and before the commit, by `python -c` over the working tree with the
same split as `wc -w`.

| Figure | Command | Result |
|---|---|---|
| must-fixes after round 1, and how many sat inside the previous repair | `grep -h "^\| [0-9] \| " docs/tickets/done/EM-0*.md \| awk -F'\|' '$2+0>1 && $3+0>0'` | 4 rows; must-fix cells 1, 2, 1, 1; inside cells "1 of 1", "2 of 2", "3 of 3", "1 of 1" |
| total must-fixes and rounds | `grep -h "^\| [0-9] \| " docs/tickets/done/EM-0*.md \| awk -F'\|' '{r++; gsub(/ *\(.*/,"",$3); m+=$3} END {print r, m}'` | 29 rounds, 33 must-fixes |
| tier model words, before and after | `git show 1052615:docs/tier-review-model.md \| wc -w`, then the working tree at close | 4461 → 4764 |
| policy words, before and after | `git show 1052615:docs/ai-contributor-policy.md \| wc -w`, then the working tree at close | 3189 → 3226 |

Five is derived from the four rows' must-fix cells, and "five of five" from
their inside cells, each of which says all of that row's must-fixes sat
inside the previous repair; EM-016's row counts findings rather than
must-fixes in that cell, and its one must-fix was among them. The totals
are derived from the rows and not asserted beside them. `5d94db7`,
`EM-016`, `§7` and the round numbers name things and are outside the rule
that requires a command.

### Falsification
N/A — no behavioural claim. What a reader does differently, per criterion:
- AC1: an executor handing back a repair reads the section, not the diff,
  and catches the sentence beside the one it fixed.
- AC2: an executor at claim reads the ticket against itself and blocks on a
  contradiction instead of transcribing one side of it.
- AC3, AC4: a reviewer knows where the rule is and what would retire it.
- AC5: an executor stops re-flowing, and a reviewer stops flagging line
  length.

### Departure from Behaviour, recorded
Behaviour bullet 4 dictated the falsifier's wording: retired when
must-fixes after the first round sit inside the previous repair "as often
as they did before it". Round 1 found that a baseline of five of five is a
ceiling, so the wording could match only at exactly one hundred percent
again, and a single ordinary round-2 finding would have made the rule
unretirable for good. The landed line counts instead: more than once over a
stated population of tickets closed under the rule, against five over
thirteen reviewed tickets at 5d94db7. The decision the falsifier expresses,
retire when the read buys nothing, is unchanged; the measurement is
corrected. Recorded here rather than raised as a BLOCKER on the precedent of
EM-007 and EM-014-001, both accepted by the maintainer, and because the
maintainer asked for fewer rounds; the maintainer may reinstate the ratio by
amending the line, which is critical work and its own ticket.

### Out of scope (per ticket)
Confirmed: what a review reports and when it ends are unchanged; no
existing text was re-flowed — the only re-flows are of the two paragraphs
this ticket wrote, which the rule permits; no machine check was added.

Beyond the Files list and declared here: the index row for "When review
ends" in "What is in this document", one line, required by EM-016's
same-commit rule because the section now settles one more thing.

### Review
| Round | Must-fix | Where (rules / lists / documents / tests) | Inside previous round's fix | Repaired by |
|---|---|---|---|---|
| 1 | 1 (of 11 findings) | documents: the falsifier's baseline was a ratio already at its ceiling, so the rule could never retire (must-fix); the wrapping clause and the claim-time arm carried no retirement clause of their own; the checklist item named the document and not the section; the description's derivation of five-of-five and the closing commit's effect on the count; the 22-mentions figure without its exact pattern; "had read one sentence" as inference; the wrapping clause's reach; "the section" undefined at a boundary; the claim-time triple omits Acceptance criteria and Out of scope; the re-flow clause and the wrapping clause against the closed records, both passing | — | 56cd2ef, afdbaa4 |
| 2 | 0 (of 3 notes) | documents: "more than once" is an absolute count with no rate, recorded and not taken since it is the documents' idiom; §3 carries two falsifiers and the line named neither; the ticket's Context named four words for a six-alternative pattern | 3 of 3 | the closing commit (two); recorded (one) |

Derived total: 1 must-fix over two round(s).
Round 1 by column and rule — permits: R1.1, this rule's falsifier (a
ratio at its ceiling; remedy: a count against a stated population, the
departure recorded above); R1.2, "Retiring a control" (the wrapping clause
and the claim-time arm carried no falsifier; remedy: one clause each);
R1.3, the checklist item (named the document, not the section); R1.4, §6's
baseline bullet (the derivation of five of five, given above, with the note
that EM-016's cell counts findings, a defect in a closed record and out of
scope here); R1.5, §6's command bullet (the 22-mentions figure named no
pattern; the ticket now states it, and the reviewer reproduced 22 from it);
R1.6, §6's obtained-figure clause ("had read one sentence" was inference;
now "the repair had touched one"); R1.7, the wrapping clause's reach (now
within a paragraph or between them). Refuses: R1.8, "the section" (now the
whole `##` section of each touched document); R1.9, the claim-time triple
omits Acceptance criteria and Out of scope — recorded, with this ticket as
the instance: its AC3 and Behaviour bullet 2 disagreed on where the rule is
stated and were reconciled by judgement in e6d9081, which item 2 as worded
would not have caught; R1.10 and R1.11, the re-flow and wrapping clauses
against the closed records, both passing. Round 2's three notes sat inside
round-1 remedies; two are taken at close and one recorded.

**The practice this description is the third instance of.** Round 2 named
it: a review must-fix whose remedy is stated, on a sentence the ticket's
Behaviour dictates, is taken in the round and recorded under this heading
rather than blocked under §3 — EM-007, EM-014-001, and now this ticket,
the first two accepted by the maintainer. Three instances clear the bar
EM-021 lands next, so §3 either gains the clause or the practice stops.
Raised as EM-020-001, in `ready/`, not decided here.

Also noted in round 2: afdbaa4 re-wrapped sentences inside the paragraph
this branch wrote at a74b0cb, which the rule permits — no baseline line of
blame moved — and the executor's own whole-section read before round 1
found two defects the reviewer then did not have to.
Post-review tree check after each round: `git status --porcelain` empty,
`git worktree list` showing only the main tree.

### How to verify
1. `grep -n "read whole" docs/tier-review-model.md docs/ai-contributor-policy.md`
   — the rule once in the model, the reference once in the checklist.
2. Re-run the two `grep | awk` commands above.
3. `git diff 1052615..HEAD --stat` — two documents and ticket housekeeping.

### Risks / follow-ups
- The rule is a discipline, and a discipline is enforced by the next
  round's findings. Its falsifier is the count that would show it is not
  being followed.
- This ticket is EM-021's first test: it clears the second-instance bar
  with five instances across four tickets, and was landed first so that
  the bar's first application was to a rule that passes it.

