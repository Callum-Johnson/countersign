---
id: EM-024
title: A count written into prose has no falsifier and drifts silently
status: in-progress
tier: critical
complexity: M
dependencies: []
claimed_by: claude-opus-5
claimed_at: 2026-09-08
---

# EM-024 — A count in prose has no falsifier

## Context

`docs/ai-contributor-policy.md` §6 already says that a measured number comes
from a command the description names, run after the last commit that changes
it, and that a contributor never counts by hand. The rule exists. What it does
not have is anything that notices when it is broken, and the failure is silent:
prose that says "seven" where the tree holds nine reads exactly like prose that
is right.

On 2026-09-08 the control-plane project recorded **four instances in one day,
in four different tickets**, each found by an independent reviewer and each
costing a review round:

- **OMN-024, finding R4.2.** A boolean's count read "seven" where it is nine
  and "three of the seven" where it is four, in four sites: the pull-request
  description's member 4, its round-3 left-claims bullet, and the docstring and
  the failure message of `tests/unit/test_gate_results.py`. The round's own
  repair **re-created the claim it was repairing**. That ticket's record notes
  the count had then been wrong for **five consecutive rounds**.
- **OMN-022-002, finding R7.4.** A finding line said "18 sites" where the file
  and the section it referred to both said 17. Resolved to **17** by
  `git grep -c "cause=" -- src/omnissiah/dispatch/transitions.py` at `5e89931`,
  cross-checked with a second command. *(Reproduced while raising this ticket:
  the command returns 17.)*
- **OMN-022-003, finding R7.3.** A Risks paragraph asserted a cost "beyond the
  stat" for a healthy estate; the reviewer recorded it as the section's only
  unmeasured number, against a paragraph in the same section that does state
  its own figure as unmeasured.
- **OMN-020-001.** An acceptance-criterion note said "seven tests are
  Windows-only" where the executor's own later measurement, by a command it
  names, returned a different number; corrected in place with the command
  recorded.

The shape is the same in all four: a number that describes the tree is written
into a sentence, the tree moves, and nothing goes red. Three of the four were
found only because a reviewer chose to re-measure something the record asserted;
the fourth was found by the executor auditing its own prose. None was found by
a gate.

Two further facts about the shape, both from the same day's records. A count in
prose is **duplicated**: OMN-024's lives in four places and OMN-022-002's
finiteness claim in two, and a repair that corrects one copy leaves the others
standing — OMN-022-002's round-7 executor found a second copy of a disproved
claim still in the file after the first had been corrected. And a count in prose
is **self-referential** more often than it looks: OMN-024's whole difficulty is
that the sentences asserting what a search returns are themselves text the
search reads.

**A fifth instance, surfaced after this ticket was raised, and judged in
class.** The control-plane project's board, `docs/tickets/README.md`, said
"Nothing is blocked." in prose while a table higher in the same file carried a
`blocked` row, and had carried it since `91e14c2`. Both readings are taken at
that commit: `git show 91e14c2:docs/tickets/README.md | grep -n "Nothing is
blocked"` returns line 170, and `git show 91e14c2:docs/tickets/README.md |
grep -n "OMN-022-003 | blocked"` returns line 75. It is the same class rather
than a different one — zero is a count that describes the tree, the table is
the site that measures it, and the sentence restated the count instead of
pointing at the table. It is the first instance in which both sites sit in one
file, which is the fact worth adding: proximity does not help, because a
reader with both on one screen still cannot see the disagreement without
reading the table as data. The prose has since been corrected; the commits
that touched it are listed by `git log --oneline --all -S'Nothing is blocked'
-- docs/tickets/README.md`.

The second-instance bar in `docs/ai-contributor-policy.md` — a rule needs a
second instance before it is written — is met four times over, in one day, on
one project. This ticket does not claim the bar needs relaxing; it claims it has
been cleared.

## Specification

The shape, not the answer. **A prior question belongs to the maintainer and
should be put to them before the work is designed**, because the two readings
lead to different documents and different obligations.

**The prior question: is an unmeasured count a review obligation or a
structural one?**

1. **A review obligation.** "What a review reports" gains a line: a reviewer
   reproduces every number a record asserts about the tree, or records that it
   did not. Cheapest, and it puts the cost on every review for ever, which is
   the resource the round cap exists to protect. It also leaves the defect
   reachable — a reviewer who does not re-measure finds nothing, which is
   exactly what happened for five consecutive rounds on OMN-024.
2. **A structural rule.** A count that describes the tree does not live in
   prose at all: it lives in a test that measures it, and the prose points at
   the test. The number then has a falsifier — the test goes red when the tree
   moves — and the duplication problem disappears, because there is one site.
   Strongest, and it costs a test per count and forces the question of which
   counts are worth one.
3. **Both**, with the review obligation as the floor and the structural rule
   for a count a document asserts more than once.

Whichever is chosen, two things the evidence says the answer must handle:

- **Duplication.** A rule that corrects a count where it is read does not help
  when the count is written in four places. The answer says what happens to the
  other three.
- **Self-reference.** Where the count describes a search over a tree that
  contains the sentence, the instrument has to exclude prose — which is what
  OMN-024 spent three rounds discovering, and it is a general fact about this
  class rather than that ticket's own difficulty.

### Files

- `docs/ai-contributor-policy.md` §6 — where the existing rule lives
- `docs/tier-review-model.md`, "What a review reports" — if the answer is 1 or 3
- `docs/quality-gates.md` — if the answer is 2 or 3, since a count with a test
  is a pinned claim and belongs beside "A test pins a claim, not a mechanism"
- `templates/PR-DESCRIPTION.md` — if what a description must carry changes

### Public surface

Every one of these is an instruction an adopter follows. A rule that makes
every review heavier is a cost paid by every adopting project on every ticket,
which is the reason the prior question is the maintainer's and not an
executor's.

### Behaviour

- The rule states what a reader does differently, not only what a writer must
  do. §6's existing sentence binds the writer and has been broken four times in
  a day; the answer says who notices.
- The map in `ai-contributor-policy.md` and the model's index are updated in the
  same commit, per the map/index same-commit rule, if a rule-bearing section is
  added or re-scoped.
- **This ticket states no rule of its own**, so it states no falsifier of its
  own. The falsifier belongs to whichever rule the answer lands.

### Falsifier

Per "Retiring a control", for the rule this ticket's answer adds: retired when,
over a stated population of reviews, no reproduction of a record's asserted
number finds one wrong — the obligation would be costing a step and catching
nothing. The population must be stated, because the whole evidence for the rule
is a single day on a single project.

## The maintainer's answer

Given 2026-09-08, in answer to the prior question above, and recorded here
before the design was built. Quoted rather than summarised.

> **Structural — a count lives in a test.** A count that describes the tree
> does not live in prose: it lives in a test that measures it, and the prose
> points at the test. The number then has a falsifier — the test goes red when
> the tree moves — and the duplication problem disappears, because there is
> one site.

That is option 2, chosen over the review obligation and over both, on the
stated reasoning that it is the only option that fixes duplication — which is
what actually defeated OMN-024, where the count lived in four sites, a repair
corrected one copy and left three standing, and the round's own repair
re-created the claim it was repairing.

The answer settles the reserved question and is not the executor's to revisit.
What it leaves to the executor is where the rule lands, how it states the
duplication and self-reference clauses the Specification demands of any answer,
what it says a **reader** does, and what the rule does not reach.

## Acceptance criteria

1. AC1: the maintainer's answer to the prior question is recorded in this ticket
   before the design is built.
2. AC2: the rule the answer lands states its falsifier and the population it is
   measured over.
3. AC3: the four instances above are cited as the second-instance evidence, each
   naming the ticket and the finding, so a later reader can judge whether the
   bar was cleared rather than take this ticket's word.
4. AC4: the answer says what happens to a count duplicated across sites, and
   what instrument settles a count whose subject includes the sentence stating
   it.
5. AC5: no existing rule is silently widened. If §6's sentence is replaced
   rather than extended, the replacement is recorded as such.

## Out of scope

- The four control-plane tickets themselves. Each records and repairs its own
  count; this ticket is about the rule, not the instances.
- Any general rule about duplicated prose. The evidence is about counts, and a
  rule about duplication generally would be reaching past what was measured.
- Retrospectively auditing every number in either project's existing records.
  That is a sweep, and whether it is worth doing is a consequence of the answer
  rather than part of it.

## References

- `docs/ai-contributor-policy.md` §6 — the existing rule, and the one broken
- `docs/tier-review-model.md`, "What a review reports" — where a review
  obligation would land
- `docs/quality-gates.md`, "A test pins a claim, not a mechanism" — where a
  structural rule would land
- The control-plane project's OMN-024 (R4.2), OMN-022-002 (R7.4), OMN-022-003
  (R7.3) and OMN-020-001, all on 2026-09-08 — the four instances

## Notes

Raised on 2026-09-08 from four findings on one project in one day, by the agent
that commissioned the reviews that found them. Three of the four were found by a
reviewer choosing to re-measure; the fourth by an executor auditing its own
prose. **None was found by a gate**, which is the fact the ticket rests on.

Proposed `standard`: the change alters an instruction an adopter follows.
The tier question EM-007-002 owns applies here as to every documentation ticket
on this board; the executor may raise and never lower, so the higher tier is the
one an author can propose without resolving it.

**Tier raised from `standard` to `critical` by the executor on 2026-09-08**,
under "Separation of duties" in `docs/tier-review-model.md`: this change adds a
rule to a process document, and `docs/adr-process.md`, "What \"a workflow rule
changes\" reaches", states that a rule added to a process document is a
process-surface change under the operative test either way — clause 5. Only a
reviewer may lower it.

## PR Description

> Leave this section empty when authoring the ticket.
