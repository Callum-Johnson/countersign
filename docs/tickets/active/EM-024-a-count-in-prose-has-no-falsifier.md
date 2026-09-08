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
rule to a process document, and `docs/adr-process.md`, "What a workflow rule
changes reaches", states that a rule added to a process document is a
process-surface change under the operative test either way — clause 5. Only a
reviewer may lower it.

## PR Description

### Ticket
EM-024 — A count written into prose has no falsifier and drifts silently

### Tier
`critical` — raised from the author's proposed `standard` by the executor on
2026-09-08, under "Separation of duties": the change adds a rule to a process
document, and `docs/adr-process.md` states that a rule added to a process
document is a process-surface change under the operative test either way,
which is clause 5. The one-line reason is in the ticket's Notes. Only a
reviewer may lower it, and the round-1 reviewer judged the raise correct
rather than lowering it.

**One independent review round has run.** The executor does not review its own
work; the round-1 record and its repair are in the Review section below. The
ticket stays `in-progress` in `active/` pending round 2 under ADR-0002.

**No decision record is owed.** `docs/adr-process.md`, "What a workflow rule
changes reaches", puts a rule added inside a document, under an existing
decision, on the second side of the line: it stays in the document with its
falsifier and its ticket is its record. This rule is added inside
`docs/quality-gates.md` under the falsification gate's existing decision that
the executor pins claims before reporting, and extends policy §6 in place. The
round-1 repair renames and restates that section but adds no rule and moves no
rule between documents, so it does not change the answer; it is the same shape
as EM-011's and EM-021's, which the section names as producing no record.

### Summary
`docs/quality-gates.md` gains a section beside the falsification gate: a count
that describes the tree has exactly one site, and that site is one that goes
red when the tree moves — a test where the project has a suite, and where it
has none, no number at all. Prose names the site rather than restating the
number. Where the count's subject includes the sentence stating it, the
instrument excludes prose, because a text search returns the sentence. The
section states which numbers it reaches by a test rather than by enumeration,
what a reader does, what the degraded form on a project with no suite costs,
what it does not reach, and its falsifier with the population named. Policy
§6's measured-number bullet is extended, not replaced, and says so.

**The round-1 review found the rule's own commit carrying the defect the rule
forbids, at every site finding R1.1 below enumerates, one of them a line that
commit had just rewritten. That is recorded here as the ticket's strongest
evidence rather than as an embarrassment; the paragraph is at the end of the
Review section.**

### Acceptance criteria

- [x] **AC1: the maintainer's answer is recorded in this ticket before the
  design is built.** The ticket's section "The maintainer's answer" quotes it
  in full and dates it 2026-09-08. It was committed at `cedb7a8`, before the
  rule commit `19cbb74`; `git log --oneline --reverse 8abf61a..HEAD` shows the
  order. The round-1 repair does not revisit it: the answer settled which of
  the three options the rule implements, and restating that option at the level
  of its own two properties is not a fourth option. The reasoning is under
  "The structural finding" in Review.
  *What a reader does differently:* a reader of the ticket sees which of the
  three options the rule implements, and on what reasoning, without asking the
  maintainer or inferring it from the diff.

- [x] **AC2: the rule states its falsifier and the population it is measured
  over.** `docs/quality-gates.md`, "A count that describes the tree has one
  site that goes red", closes with a **Retired when:** line whose population is
  **reproductions of a number a record asserts about the tree**, not closed
  tickets. The round-1 review found the earlier population unobservable —
  closed tickets are counted, reproductions are not, so a retirement read from
  closed tickets fires on silence and fires hardest where the section is
  followed least. The line now says a reproduction counts towards the
  population when it is recorded, that a project recording none never reaches a
  population, and — in terms — that the section asks for no reproduction. Fifty
  is written as a default and named as one, and the line states that the whole
  evidence is a single day, 2026-09-08, on a single project.
  *What a reader does differently:* a maintainer can retire the section on
  evidence rather than on taste, and can see that the evidence base is one day
  and not a history; and a maintainer who finds the falsifier's population at
  zero knows the control was never tested, rather than reading zero failures as
  the control catching nothing.

- [x] **AC3: the four instances are cited as the second-instance evidence,
  each naming the ticket and the finding.** They are the bulleted entries in
  the ticket's Context, unchanged from the raise. A fifth, judged in class, is
  added as the paragraph that follows them. The enumeration, rather than a
  count of it, is read from
  `grep -n '^- \*\*OMN\|^\*\*A fifth instance' docs/tickets/active/EM-024-a-count-in-prose-has-no-falsifier.md`
  at `32bcd29` and again at the commit carrying this description, which does
  not touch the lines it reads; both return:

  ```
  27:- **OMN-024, finding R4.2.** A boolean's count read "seven" where it is nine
  33:- **OMN-022-002, finding R7.4.** A finding line said "18 sites" where the file
  38:- **OMN-022-003, finding R7.3.** A Risks paragraph asserted a cost "beyond the
  42:- **OMN-020-001.** An acceptance-criterion note said "seven tests are
  62:**A fifth instance, surfaced after this ticket was raised, and judged in
  ```

  The count "four" appears in this description exactly where the template
  requires the ticket's acceptance criterion to be copied verbatim, which is
  the line above and the ticket's own AC3. The description asserts no count of
  the instances on its own account, the evidence block is their one site, and
  the new section states none. The round-1 review found the earlier wording
  here — that the description stated no count of them — false against its own
  heading; this is the correction. Which of the citations can be reproduced
  from a tree, and which are names a reader cannot open, is under Risks.
  *What a reader does differently:* a reader judges whether the second-instance
  bar was cleared by reading the instances, instead of taking the ticket's word
  for a number.

- [x] **AC4: the answer says what happens to a count duplicated across sites,
  and what instrument settles a count whose subject includes the sentence
  stating it.** Two paragraphs of the section, in those terms, plus a third the
  round-1 review required.
  Duplication: "One site, and every other mention names the site rather than
  the number", with OMN-024's four sites named and the note that the repairing
  round re-created the claim it was repairing; under the section a number found
  in a second place is a defect on its face, visible without measuring
  anything. Self-reference: "Where the count's subject includes the sentence
  stating it, the instrument excludes prose", stating that a text search
  returns the sentence, that restricting the search to source paths does not
  fix it because a docstring is under `src/` too, and that a parser settles it
  because to a parser a docstring is a string constant and never a call. The
  third, added at round 1: what the duplication clause costs where nothing goes
  red, which is that it is enforceable only by a reader who looks.
  *What a contributor does differently:* a contributor with a count writes it
  once and points at it, and repairs it in one place rather than three; a
  contributor with a claim of absence over its own tree reaches for a parser
  first, instead of spending the rounds OMN-024 spent; and a contributor in a
  repository with no runner knows the clause is weak there and reaches for the
  form with no number rather than trusting it.

- [x] **AC5: no existing rule is silently widened; a replacement is recorded as
  such.** §6's measured-number bullet is **extended, not replaced**, and says
  so in the bullet itself: "This bullet is unchanged and still reaches every
  measured number, counts included." The diff against the branch point shows no
  deletion in §6 beyond the lines the insertion re-flows —
  `git diff --stat 8abf61a..b732abe -- docs/ai-contributor-policy.md` is the
  command.
  Two changes at round 1 are recorded here as changes rather than left to be
  found in the diff. **The section was renamed**, from "A count that describes
  the tree lives in a test" to "A count that describes the tree has one site
  that goes red", and its rule sentence restated at the level of its two
  properties; the reasoning is under "The structural finding" in Review. Every
  reference to the old title moved in the same commit — `git grep -n
  "describes the tree lives in a test" -- README.md DISCLOSURE.md docs
  templates ':(exclude)docs/tickets'` returns nothing at `f674e67`. The
  exclusion is not tidying: without it the command returns this sentence,
  because the sentence claiming the phrase is gone contains the phrase. That is
  the section's own self-reference clause met in its own description, and it is
  left visible rather than worked around silently. The words "lives in a test"
  also survive in this ticket's Specification and in the maintainer's quoted
  answer, where they are the option as it was written and as it was answered,
  not a reference to a section title, and are not edited. **The section's scope is now
  stated as a test rather than an enumeration**: it previously excluded a
  duration, a version and a date by listing them, which left a contributor
  unable to place a percentage or a stipulated constant. The test is whether
  the tree could move so that the number becomes wrong without anyone editing
  the sentence. That is a narrowing and a widening at once — percentages come
  in, stipulated constants go out — and both are stated in the section rather
  than inferred.
  Nothing else in `docs/` is narrowed or widened, and
  `docs/tier-review-model.md` is untouched:
  `git diff --stat 8abf61a..HEAD -- docs/tier-review-model.md` reports no
  change.
  *What a reader does differently:* a reader of §6 who has read it before finds
  the bullet they remember, plus a sentence telling them what was added and
  that the old obligation is undiminished; and a reader who knew the section
  under its old name is told the name changed and why, rather than meeting a
  section that reads as a different rule.

### Measured figures, each with its command
Every command below was run at `b732abe`, the last commit that changes what any
of them counts, against the baseline `8abf61a`, this branch's point off `main`.
The commits after it touch only ticket files and the board, which none of these
figures counts.

| Figure | Command | Result |
|---|---|---|
| quality gates, words before | `git show 8abf61a:docs/quality-gates.md \| wc -w` | 2229 |
| quality gates, words after | `git show b732abe:docs/quality-gates.md \| wc -w` | 3827 |
| policy, words before | `git show 8abf61a:docs/ai-contributor-policy.md \| wc -w` | 3266 |
| policy, words after | `git show b732abe:docs/ai-contributor-policy.md \| wc -w` | 3388 |
| PR template, words before | `git show 8abf61a:templates/PR-DESCRIPTION.md \| wc -w` | 876 |
| PR template, words after | `git show b732abe:templates/PR-DESCRIPTION.md \| wc -w` | 957 |
| README, words before | `git show 8abf61a:README.md \| wc -w` | 1044 |
| README, words after | `git show b732abe:README.md \| wc -w` | 1052 |
| rule-bearing files changed | `git diff --stat 8abf61a..b732abe -- README.md docs/ai-contributor-policy.md docs/quality-gates.md templates/PR-DESCRIPTION.md \| tail -1` | 4 files changed, 149 insertions(+), 5 deletions(-) |

The rule costs this repository 1,809 words across those files, by subtraction
from the rows above and asserted nowhere else. Round 1 added 731 of them, by
the same subtraction against the same rows at `19cbb74`.

`EM-024`, `§6`, `AC3`, `8abf61a`, `19cbb74`, `b732abe`, `32bcd29` and the line
numbers in the AC3 block name things or locate them rather than measure a
population, and are outside §6's measured-number bullet by the test that bullet
states and outside the new section by the test it states.

### The gate this repository has
**It has none, and this section says so rather than implying a check that does
not exist.** The machine gates in `docs/quality-gates.md` are the process this
repository publishes for adopting projects; this repository ships Markdown and
has no runner for any of them. At `32bcd29`:

| Question | Command | Result |
|---|---|---|
| Python sources? | `git ls-files \| grep -Ec '\.py$'` | 0 |
| Any script or config a gate could run? | `git ls-files \| grep -Eic '\.(ya?ml\|toml\|sh\|cfg\|ini)$\|(^\|/)(Makefile\|justfile\|\.pre-commit-config\.yaml)$'` | 0 |
| CI configuration? | `git ls-files \| grep -c '^\.github/'` | 0 |
| What is tracked at the top level? | `git ls-files \| cut -d/ -f1 \| sort -u` | `.gitignore`, `DISCLOSURE.md`, `LICENSE`, `README.md`, `case-studies`, `docs`, `examples`, `templates` |

There is no `scripts/` directory, and round 1 added none: the sweep's
instrument is written out in EM-024-002's Context so that a reader can
reproduce it, rather than committed as a file this repository does not run.
`ruff`, `mypy` and `pytest` have nothing here to run against, and reporting
them as passed would be false.

The one mechanical check this repository does have is the directory/status
invariant, and it was run. The command, at `32bcd29`:

```sh
for f in docs/tickets/*/*.md; do
  d=$(basename $(dirname "$f"))
  s=$(grep -m1 '^status:' "$f" | sed 's/status: //' | tr -d '\r')
  case "$d:$s" in
    ready:ready|active:in-progress|blocked:blocked|done:done) ;;
    *) echo "MISMATCH $f dir=$d status=$s" ;;
  esac
done
```

It printed nothing over the ticket files that `ls docs/tickets/*/*.md | wc -l`
counts at that commit, which is the invariant holding. EM-024 is
`status: in-progress` in `docs/tickets/active/`, EM-024-001 and EM-024-002 are
`status: ready` in `docs/tickets/ready/`.

### Falsification
N/A for a behavioural claim — this change makes none, and there is no suite.
What a reader or contributor does differently is stated per acceptance
criterion above, which is the form `templates/PR-DESCRIPTION.md` gives for a
change with no behavioural claim.

Per repaired review finding, the class and its siblings, in policy §6's form.
The change has no suite, so each sibling says what a reader would do
differently instead of naming a test and a red count.

- **R1.1 — class: which sentences in this repository's rule-bearing documents
  state a number that counts something in this tree?** Not "the gate count",
  which is the instance. Swept mechanically; the instrument, its output and its
  blind spots are written out in EM-024-002's Context, and the sweep is quoted
  there rather than summarised. Siblings beyond the five gate-count sites:
  `docs/ai-contributor-policy.md:16` ("searching five documents"), `:332`
  ("tick all seven"), `docs/ticket-lifecycle.md:188` ("Three things the scheme
  does not say"), `docs/tier-review-model.md:26` and `:27` (index rows
  restating counts of lists in sections of the same document), `README.md:38`
  ("Three risk tiers"), and `docs/tier-review-model.md:359` ("five of five").
  One more, `docs/adr/0003-...:100`, is in class and outside the population,
  and is named in EM-024-002 as seen and left. All are raised, none repaired
  here, per §4.
  *What a reader does differently:* a reader who wants to know whether this
  repository complies with its own new section runs one command and reads a
  list, instead of taking the executor's word that the sites it was handed were
  all of them.
- **R1.2 — class: which numbers in `docs/tier-review-model.md` state a count of
  this repository with no site?** `grep -n "thirteen" docs/tier-review-model.md`
  at `de99c4e`, the last commit that changes that file, returns lines 374 and
  489: both are in EM-024-001, which now covers both. The wider sweep in R1.1
  covers the same document for the rest of the class.
  *What a reader does differently:* a reader of EM-024-001 who repairs the
  sentence it was raised for does not leave a second copy of the same defect
  three hundred lines away in the same file.
- **R1.3 — class: which command written into this branch's ticket files returns
  nothing when it is run?** Every backticked command in the three ticket files
  on this branch was extracted and run, except those that address the
  control-plane repository and cannot be run from here. The one that returned
  nothing was EM-024-001's, and it is the only one: the AC3 enumeration
  command, `grep -n "thirteen"`, the gate-block command, the Review-table
  command at `5d94db7`, the `git ls-files` gate questions, the
  governed-documents command, the word counts in Measured figures and the
  ticket-file count all return output at `32bcd29`.
  *What a reader does differently:* a reader who runs a command a ticket names,
  in order to check a number the ticket asserts, gets output rather than
  silence — and silence from a grep reads as "nothing to find", which is the
  wrong answer given loudly.
- **R1.4 — class: which claim this description makes about its own text is
  false?** Two, and they are the same defect: AC3's "this description states no
  count of them", against "the four instances" in its own heading; and "How to
  verify" step 3, which said "the two places in the template that already
  pointed at §6" where `grep -c "§6" templates/PR-DESCRIPTION.md` returns 3 at
  `b732abe`. Both are repaired above and below. The third self-referential
  claim, step 6's "this description restates no count that has a list", is now
  true of the enumeration and is stated as a check a reader runs rather than as
  a fact the description asserts.
  *What a reader does differently:* a reader checking the description against
  itself finds the checks pass, and a description whose self-description is
  wrong is exactly the failure this ticket is about, one level up.
- **R1.5 — repair of the instance.** The falsifier's population. The section
  states one falsifier and it is the one repaired; the sweep for others is
  the class question "which falsifier in this repository names a population
  nothing records?", which reaches every rule in `docs/` and is EM-014's
  subject, not this ticket's. Recorded here as an instance repair, which is a
  claim round 2 can test.
- **R1.6 — repair of the instance.** The scope boundary stated as a test rather
  than an enumeration. One section, one scope paragraph.
- **R1.7 — class: which number in the new section's own text has no site?**
  The section was swept with the same instrument as R1.1, over its own line
  range. What remains is "one", "two" and "one of them" used as enumerative
  words rather than counts; the seven-and-nine illustration; "five of them" and
  "the three conditions" quoted as examples of the form the section rejects;
  OMN-024's round 3, which names a round rather than measuring one; and
  "fifty", a default named as one in the falsifier. "OMN-024 spent three
  rounds" is gone — `grep -n "three rounds" docs/quality-gates.md` returns
  nothing at `32bcd29`.
  *What a reader does differently:* a reader who applies the section to the
  section finds it complies, which is the least a rule of this kind can offer.
- **R1.8 — with R1.4.** Step 3's count.

### Out of scope (per ticket)
Confirmed, one line each:

- **The four control-plane tickets themselves.** None was opened for editing;
  the control-plane repository was read only, and not at all during round 1.
- **Any general rule about duplicated prose.** The section refuses this in
  terms: two sentences saying the same thing are a matter of style until one of
  them is a number about the tree. §5's bar on speculative abstraction is the
  reason, and the section's "What this section does not reach" paragraph is
  where the line is drawn. Round 1 tested that boundary once more and held it:
  the wrap blindness that hid two sites from two different greps is recorded in
  that paragraph as an instrument property and explicitly **not** made a rule,
  because the second-instance bar is not cleared by two instances in one round.
- **Retrospectively auditing every number in either project's records.** None
  was audited. The round-1 sweep reads the rule-bearing documents the map
  governs — the population the section binds first — and not `docs/tickets/`,
  `docs/adr/`, `case-studies/` or `examples/`. Its findings are raised as
  EM-024-002 under §4 and are not repaired here.

Also confirmed: the rule was not made a review obligation. The maintainer's
answer chose the structural option over that one, the round-1 repair says so in
the section itself, and `docs/tier-review-model.md`, "What a review reports", is
untouched — `git diff --stat 8abf61a..HEAD -- docs/tier-review-model.md`
reports no change.

### How to verify
1. Read `docs/quality-gates.md`, "A count that describes the tree has one site
   that goes red", in full — it is one section and states its own scope test,
   its degraded form, what that form costs, and its falsifier.
2. `git diff 8abf61a..b732abe -- docs/ai-contributor-policy.md` — check that
   §6's bullet is extended and nothing in it is deleted, and that the map row
   for the quality gates sends the question "where does a count that describes
   the tree live?" to the right document.
3. `git diff 8abf61a..b732abe -- README.md templates/PR-DESCRIPTION.md` — the
   index line, and the places in the template that already pointed at §6. The
   template's mentions of §6 are enumerated by
   `grep -n "§6" templates/PR-DESCRIPTION.md`; the diff shows which of them the
   change touched.
4. `git diff 5a861a9..HEAD` — the round-1 repair on its own, which is the diff
   round 2 reads.
5. Re-run every command in "Measured figures", "The gate this repository has"
   and the Falsification section. They are the only numbers here.
6. Run the sweep in EM-024-002's Context. It is the instrument this round used;
   its blind spots are stated beside it, and a reader who wants to know what
   this repository still owes reads its output rather than this description.
7. `git show 91e14c2:docs/tickets/README.md | grep -n "Nothing is blocked"` and
   `... | grep -n "OMN-022-003 | blocked"`, in the control-plane repository, for
   the fifth instance's two sites in one file.
8. Check that this description restates no count that has a list: the instances
   are enumerated and never totalled, and the gate count's sites are enumerated
   in EM-024-002 and never totalled, which is the section applied to itself.

### Risks / follow-ups
- **The degraded form is genuinely weaker, and this repository lives in it.**
  With no suite, a count's one site is a command in a document, which runs when
  a reader chooses to run it. Nothing goes red here. Round 1 required the
  section to say what that costs rather than only that it is weaker, and it now
  does: the one-site clause becomes enforceable only by a reader who looks,
  which is the shape of the option the maintainer chose against. The section's
  answer is to prefer no number at all in a repository of documents, which
  removes the thing a reader would have to find. Where a number is written
  anyway the weakness stands.
- **Three of the five citations could not be reproduced from a tree.** In the
  control-plane clone available while working this ticket, `main` at `a1d16ff`
  holds OMN-024, OMN-022-002, OMN-022-003 and OMN-020-001 in `ready/`, and
  `git grep -n -E "R4\.2|R7\.4|R7\.3" <branch> -- docs/tickets` over the three
  ticket branches returns nothing: those review records live where the reviews
  ran and have not landed. The second-instance bar permits this — "a name a
  reader cannot open is still a name, quoted with its round" — and the
  citations are quoted with their rounds. What *is* reproducible is recorded:
  the fifth instance's two sites by the commands in Context, and OMN-022-002's
  17 by `git grep -c "cause=" 5e89931 -- src/omnissiah/dispatch/transitions.py`.
  A reviewer weighing whether the bar was cleared should know which is which.
- **The ticket's AC3 says "the four instances" and the Context now carries
  five.** The fifth was added after the raise and judged in class; the
  acceptance criterion was not rewritten, because the criteria are the author's
  and the executor does not restate them to suit the work. The criterion is met
  as written — the four are cited — and the fifth is additional. A later reader
  who finds the mismatch should read it as the ticket's own instance of the
  defect it is about, in the one place the executor may not repair it.
- **EM-015 is an adjacent instance that this section deliberately does not
  reach.** The README's two commit counts for one project are figures about a
  private project's history that no command in this repository can produce.
  They are §6's, not this section's. The scope test is the one the section
  states: could a command over *this* tree settle the number.
- **EM-024-001 and EM-024-002 are raised and unworked.** Between them they hold
  every instance in this repository that the round-1 sweep judged in class.
  Neither is a sweep of the whole repository: EM-024-002's population is the
  rule-bearing documents the map governs, and its instrument's blind spots are
  written into it so that a later reader does not mistake its output for a
  clean bill.
- **The falsifier's population is a default and is unmeasured.** Fifty
  reproductions on an adopting project is a figure this project has no evidence
  for, named as a default for the reason the batch cap's ten-and-seven are, and
  the first adopting project replaces it. The change from closed tickets to
  reproductions makes the population observable but also makes it slower to
  accumulate, and on a project that records no reproduction it never
  accumulates at all. That is stated in the falsifier as the intended
  behaviour, not hidden as a limitation.
- **The tier was raised, not lowered.** The round-1 reviewer judged the raise
  correct. EM-007-002 owns the underlying question and is blocked.

### Review

| Round | Must-fix | Where (rules / lists / documents / tests) | Inside previous round's fix | Repaired by |
|---|---|---|---|---|
| 1 | 4 | documents — `README.md`, `docs/quality-gates.md`, `docs/tier-review-model.md`; tickets — EM-024, EM-024-001 | — | `b732abe`, `32bcd29` |

Findings, per round. The round-1 record as handed to the executor gave each
finding's remedy and its cost but not its column; **the column on each line
below is the executor's reading of the finding's content, and is marked as
such**, which is a gap in the record rather than in the review, and one the
next round can correct from the reviewer's own copy.

- R1.1 · permits *(column read by the executor)* · quality gates, "A count that
  describes the tree has one site that goes red" · The commit adding the rule
  restates the machine-gate count away from the code block that is its site, at
  `README.md:39` and `:85`, `docs/quality-gates.md:17` and `:18`, and
  `docs/tier-review-model.md:93` — OMN-024's exact shape, and `README.md:39` is
  a line this commit rewrote — remedy: raise a sibling ticket covering it,
  taken as EM-024-002 at `32bcd29`; cost of the remedy: none, no control is
  tightened; inside previous fix: no.
- R1.2 · permits *(column read by the executor)* · quality gates, same section,
  applied to `docs/tier-review-model.md` · A second unsited "thirteen" at lines
  373–374, in the same document and the same class as EM-024-001, left
  unraised, and drifted: 13 at `5d94db7` against 16 at `60f39fb` by
  `git grep -l "| Round | Must-fix |" <commit> -- docs/tickets/done | wc -l` —
  remedy: fold it into EM-024-001, done at `32bcd29`; cost: none; inside
  previous fix: no.
- R1.3 · permits *(column read by the executor)* · contributor policy §6, the
  measured-number bullet · EM-024-001's own locating command returns nothing,
  because "thirteen rule-adding" wraps across lines 489 and 490 — a ticket
  about unmeasured claims whose own command does not run is the same defect one
  level up — remedy: quote the wrapped phrase, done at `32bcd29` by replacing
  it with `grep -n "thirteen" docs/tier-review-model.md`, which returns both
  sites; cost: none; inside previous fix: no.
- R1.4 · permits *(column read by the executor)* · quality gates, same section,
  applied to this description · The description's AC3 said "This description
  states no count of them", which is false: "the four instances" appears in its
  own heading — remedy: reword, done at this commit; cost: none; inside
  previous fix: no.
- R1.5 · permits *(column read by the executor)* · quality gates, the section's
  **Retired when:** line · The falsifier's population is not observable: closed
  tickets are counted, reproductions are not, because nothing records them, so
  retirement fires on silence — remedy: name reproductions as the population,
  taken at `b732abe`; cost of the remedy: one recorded line per review that
  reproduces a number, and no reproduction is asked for; inside previous fix:
  no. *Note, not a must-fix; taken.*
- R1.6 · refuses *(column read by the executor)* · quality gates, "What this
  section does not reach" · Percentages and stipulated constants are unscoped:
  the section excluded a duration, a version and a date by enumeration, and a
  contributor cannot tell whether "three rounds" is a measurement or a constant
  — remedy: state the scope as a test, taken at `b732abe` as the paragraph
  "Which numbers this reaches"; cost: percentages come into scope, which is a
  tightening, and its cost is that a proportion about the tree now needs a
  site — measured nowhere in this repository, which states no such proportion;
  inside previous fix: no. *Note, not a must-fix; taken.*
- R1.7 · permits *(column read by the executor)* · quality gates, the
  self-reference paragraph · "Three rounds" ships unsited in the rule's own
  text — remedy: drop the number, taken at `b732abe`; cost: none; inside
  previous fix: no. *Note, not a must-fix; taken as the reviewer proposed.*
- R1.8 · permits *(column read by the executor)* · quality gates, same section,
  applied to this description · "How to verify" step 3 says "two places" where
  `grep -c "§6" templates/PR-DESCRIPTION.md` returns 3 — remedy: the step now
  names the grep and does not restate the count, done at this commit; cost:
  none; inside previous fix: no. *Note, not a must-fix; taken.*

**Against the review, outside the must-fix count and the two columns**, per
`docs/quality-gates.md`, "Review isolation": the round-1 reviewer's worktree is
still registered against this repository. `git worktree list` at `f674e67`
shows `A:/projects/wt/review-EM-024` at `5a861a9`, the commit reviewed, and
`git -C A:/projects/wt/review-EM-024 status --porcelain` reports nothing, so
the tree under review was not written to — the executor's own
`git status --porcelain` is empty at `f674e67`. The rule asks that such a
worktree be removed before the tree is used again; it is recorded and **not
removed here**, because the review session may still hold it and this repair
was instructed not to write outside this tree. Removal belongs to whoever ends
that session, and this line is what the record owes either way. It is the same
shape as the round-13 finding on the control-plane project's OMN-021 that the
"Review isolation" section names.

**The structural finding, and the answer.** The reviewer judged the section's
duplication answer — a number found in a second place is a defect on its face,
which a reader can see without measuring anything — enforceable only by a
reader who looks, which in a repository with no gate is the review obligation
the maintainer explicitly rejected; and that the section admitted the weakness
without admitting that it lands option 1 in the degraded case. **The finding is
correct and it is answered here rather than blocked to the maintainer.** The
reasoning: the reserved question was which of three options, and it was
answered — structural — and this repair does not revisit it. The maintainer's
own words give the two properties that make the structural option work: "the
test goes red when the tree moves", and "there is one site". Those two
properties are the rule; a test is how a project with a suite supplies them. So
the section is renamed "A count that describes the tree has one site that goes
red" and states the rule at that level, with the test as its instance. In a
documentation repository the site that goes red usually does not exist, and the
form the section now asks for first is **no number at all** — the list is the
count, the sentence names the search — which is where the reviewer's own remedy
for the unsited "three rounds" already pointed, and where most of this
repository's counts belong, since most of them describe its own document
structure. What is left is stated rather than implied: where a number is
written anyway, the one-site clause is enforceable only by a reader who looks,
that is option 1's shape arriving through the back door, and the section says
so and adds no review obligation. Restating a chosen option at the level of its
own reasoning is not choosing a fourth; had it required choosing one, §3 would
have applied and this would have blocked.

**What this round's most important finding is, stated plainly.** The commit
that added a rule forbidding unmeasured counts in prose carried that exact
defect at every site finding R1.1 enumerates, one of them a line the same
commit rewrote, and the ticket that commit raised carried a locating command
that returned nothing. That is not an embarrassment to be minimised. It is the
strongest evidence in this ticket that the rule was needed, and it is direct
evidence against the option the maintainer rejected: the record **was** audited
by its author — the ticket's own Notes say the fourth control-plane instance
was found "by an executor auditing its own prose" — and it was wrong at every
one of those sites anyway. A review obligation asks a reader to look; this
round is a measurement of what happens when the reader looking is the author,
on the one document in the world where the author was most alert to this exact
defect. What matters is not how many sites there were. It is that a mechanical
sweep run in an afternoon found sites that two careful readings of the same
documents did not, and that the sweep's own first version, written by the same
author on the same afternoon, missed one of them too.
