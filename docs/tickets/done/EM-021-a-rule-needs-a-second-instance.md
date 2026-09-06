---
id: EM-021
title: A rule needs a second instance before it is written
status: done
tier: critical
complexity: S
dependencies: []
claimed_by: claude-fable-5-1
claimed_at: 2026-09-06
closed_at: 2026-09-06
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
  findings in different tickets name the same rule and the same defect,
  they are two instances; a tighter definition is a later ticket with
  evidence.

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

### Ticket
EM-021 — A rule needs a second instance before it is written

### Tier
`critical` — process-surface change (clause 5): it adds a condition on
adding a rule to these documents.

**Independent review obtained**, per ADR-0002: a separate agent, given the
ticket, the diff and the two questions, and not the executor's reasoning,
reviewed the change in three round(s), read-only. Findings are under
Review; the tree was checked clean after each round.

### Summary
"Retiring a control" gains one paragraph before "Who this binds": a
failure, cost or finding met once is recorded where it was met and is not
written into these documents as a rule until it is met a second time; the
ticket that adds the rule names both instances; a rule preventing an
irreversible outcome may be written from one instance and says so. The
paragraph names its own instance count honestly and carries its falsifier.

**Applied to its own landing:** the executor read the whole section before
dispatching the review, per EM-020, which landed immediately before this
ticket and is this rule's first test.

### Acceptance criteria
- [x] AC1: the second-instance bar and where a first instance is recorded
  meanwhile — `docs/tier-review-model.md`, "Retiring a control", the
  paragraph beginning "**A rule needs a second instance.**"
- [x] AC2: the irreversible-outcome exception — "A rule that prevents an
  outcome that cannot be undone … may be written from one instance, and
  says so."
- [x] AC3: its own instance count — "nearly every rule in it came from one
  instance, and that is this rule's own instance count."
- [x] AC4: a **Retired when:** line — the paragraph following.
- [x] AC5: independent review — see Review.

### The figures, each with its command
The word counts are of the content the closing commit carries, taken after
its last edit to each file and before the commit, with the same split as
`wc -w`; the closing commit changes no counted file after that point.

| Figure | Command | Result |
|---|---|---|
| tier model words, before and after | `git show <rev>:docs/tier-review-model.md \| wc -w` at 89345f3, then the working tree at close | 4764 → 5147 |
| the five documents, at the wave's start and now | `wc -w` over the five files at 8b0a8b4, then the working tree at close | 3,152 → 13,325 |

`EM-006`, `EM-019-001`, `§4` and `8b0a8b4` name things and are outside the
rule that requires a command.

### Falsification
N/A — no behavioural claim. What a reader does differently, per criterion:
- AC1: an executor who meets a failure once writes it into the ticket's
  Risks or a child ticket, and does not open the policy to add a rule.
- AC2: an executor who meets an irreversible failure once writes the rule
  anyway and says why.
- AC3: a reader knows the wave's rules would not have cleared this bar, and
  that the bar applies from here forward.
- AC4: a maintainer knows what evidence would retire the bar.

### Departures from the ticket's own text, recorded
Three, all review-named, all recorded here on the precedent EM-020-001 now
asks §3 to decide on.

The ticket's Behaviour dictated the subject "A failure, a cost or a finding
met once". Round 1 found that "finding" is this document's term for a
review finding, so the bar as worded refused a round's own repair, a list
entry and an amendment under the section — the repair mechanism the model
rests on. The landed subject is "A failure met once", with a sentence
saying what the bar does not reach. Cost and observation still enter the
paragraph as the two things kept in the description rather than in a
ticket.

The ticket's Out of scope described sameness — "two findings name the same
rule and the same defect" — without the condition its Behaviour carries,
that the second instance is in a second ticket or on a second project. The
executor aligned Out of scope to Behaviour in-branch before dispatching
round 1, rather than blocking, and round 1 recorded it. It is the instance
EM-020's review predicted: the claim-time triple omits Out of scope.

The ticket's Behaviour dictated a falsifier that compared the cost of a
recurrence with the cost of carrying the rule. Round 2 found the two sides
in different units, rounds against words, so the line could never fire. The
landed line counts rounds on both sides and drops the comparison: retired
when a failure left unruled recurs and costs a review round, more than once
over a stated population. Round 3 noted that this errs on the retirable
side, since a second instance found at review usually costs a round; the
maintainer may reinstate a comparison by amendment, in one unit.

### Out of scope (per ticket)
Confirmed: no rule the wave added is retired; "the same failure" is not
defined more tightly than by name — the paragraph's condition is where the
second instance is, not what it is.

### Review
| Round | Must-fix | Where (rules / lists / documents / tests) | Inside previous round's fix | Repaired by |
|---|---|---|---|---|
| 1 | 4 (of 13 findings) | documents: the paragraph attributed both keeping-places to §4, which keeps only the ticket (must-fix); "nearly every rule came from one instance" was false by the paragraph's own definition and named no count (must-fix); the bar as worded refused a round's own repair, a list entry and an amendment (must-fix); the policy's map row did not name the question the section now settles (must-fix); Risks named as no template does; the irreversible exception did not admit a rule from none; why a second ticket or project, unstated; when the bar binds, unstated; a name a reader cannot open; the falsifier's two costs without units; the ticket's Out of scope edited in-branch; no decision record, routed; the landing-cost example's failure had a prior instance | — | 94fabdd, 6f55b5c, c33d896 |
| 2 | 2 (of 4 findings) | documents: the binding sentence copied "this section's landing ticket" from the paragraph below and so named EM-014, binding two closed tickets retroactively (must-fix); the falsifier compared rounds with words and could never fire (must-fix); the one-source list did not reproduce from its stated method; the paragraph's subject narrowed from Behaviour's wording | 2 of 2 | de99c4e |
| 3 | 0 (of 1 note) | documents: the falsifier, with its comparison dropped, retires on a low threshold — two recurrences each costing a round — which errs on the retirable side | 1 of 1 | recorded |

Derived total: 6 must-fix over three round(s).
Round 1 by column and rule — permits: R1.1, the paragraph against §4
(both keeping-places attributed to §4; remedy: which keeps which); R1.2,
the instance-count sentence ("nearly every" false by the paragraph's own
definition and no count; remedy: a count by a stated method, corrected once
more before round 2 when the executor's own whole-section read found
EM-012-001 missing from the population); R1.4, EM-016's same-commit rule
(the map row); R1.6, Risks named as no template does; R1.10, §3 (the
ticket's Out of scope edited in-branch); R1.11, the decision-record trigger,
routed; R1.12, the ticket's example. Refuses: R1.3, the bar's subject
("finding" is this document's term for a review finding, so the bar refused
the round's own repair; remedy: the bar governs a rule's entry as a ticket's
subject and does not reach a repair, a list entry or an amendment); R1.5,
when the bar binds; R1.7, the exception's reach (a rule from none); R1.8,
why a second ticket or project; R1.9, a name a reader cannot open; R1.13,
the falsifier's units.

Round 2's two must-fixes each sat inside a round-1 remedy and in the
opposite column to it — the class signal's shape in the order the model
does not name — and each was one clause: the binding sentence had copied
"this section's landing ticket" from the paragraph below and so bound two
closed tickets retroactively; the falsifier compared rounds with words.
Both repaired as the instance, said so. Round 2 also found the one-source
list not reproducing from its method, and the executor's reading had
EM-016 in and EM-019-001 out; the reviewer's had the reverse, and the
reviewer was right. Round 3 found no must-fix and one note, recorded as
the third departure above.
Post-review tree check after each round: `git status --porcelain` empty,
`git worktree list` showing only the main tree.

### How to verify
1. `grep -n "second instance" docs/tier-review-model.md` — one paragraph,
   in "Retiring a control", before "Who this binds".
2. `git diff 89345f3..HEAD --stat` — one document and ticket housekeeping.

### Routed and recorded
- No decision record for a rule added: routed to EM-019-001-001 under the
  second condition of "When review ends", which owns that question.
- The ticket's landing-cost example, EM-019-001, is one whose failure had
  a prior instance in EM-006's Notes; recorded, since the example is about
  what landing costs and not about what clears the bar.
- The index row in "What is in this document" and the map row in
  "Which document settles what" were both updated, in the commits that
  changed what the section settles, per EM-016. The index row is beyond
  the Files list and declared here.

### Risks / follow-ups
- The bar is a judgement — what counts as the same failure twice — and the
  ticket leaves that at "the same rule and the same defect, by name". The
  first ticket to argue over it is the evidence for tightening.
- The wave's rules stand. Retiring any of them is a retirement ticket with
  a matched falsifier, not this bar applied backwards.

