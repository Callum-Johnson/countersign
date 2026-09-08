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
reviewer may lower it.

**Independent review not yet obtained.** The executor does not review its own
work. Under ADR-0002 an independent pass is required before this merges; the
Review section below is empty because no round has run.

**No decision record is owed.** `docs/adr-process.md`, "What a workflow rule
changes reaches", puts a rule added inside a document, under an existing
decision, on the second side of the line: it stays in the document with its
falsifier and its ticket is its record. This rule is added inside
`docs/quality-gates.md` under the falsification gate's existing decision that
the executor pins claims before reporting, and extends policy §6 in place. It
is the same shape as EM-011's and EM-021's, which the section names as
producing no record.

### Summary
`docs/quality-gates.md` gains a section beside the falsification gate: a count
that describes the tree lives in a test that measures it, prose names the test
rather than restating the number, and the count therefore has exactly one site.
Where the count's subject includes the sentence stating it, the instrument
excludes prose — a text search returns the sentence. Policy §6's measured-number
bullet is extended, not replaced, and says so. The section states what a reader
does, what the degraded form is on a project with no suite, what it does not
reach, and its falsifier with the population named.

### Acceptance criteria

- [x] **AC1: the maintainer's answer is recorded in this ticket before the
  design is built.** The ticket's section "The maintainer's answer" quotes it
  in full and dates it 2026-09-08. It was committed at `cedb7a8`, before the
  rule commit `19cbb74`; `git log --oneline --reverse 8abf61a..HEAD` shows the
  order.
  *What a reader does differently:* a reader of the ticket sees which of the
  three options the rule implements, and on what reasoning, without asking the
  maintainer or inferring it from the diff.

- [x] **AC2: the rule states its falsifier and the population it is measured
  over.** `docs/quality-gates.md`, "A count that describes the tree lives in a
  test", closes with a **Retired when:** line: over the next fifty closed
  tickets on a project that has adopted the section, no reproduction of a
  number a record asserts about the tree finds one wrong. Fifty is written as
  a default and named as one; the line states in terms that the whole evidence
  is a single day, 2026-09-08, on a single project, and that the first adopting
  project's fifty closed tickets replace the figure. Fifty is not a measured
  number and is not offered as one.
  *What a reader does differently:* a maintainer can retire the section on
  evidence rather than on taste, and can see, before adopting it, that the
  evidence base is one day and not a history.

- [x] **AC3: the four instances are cited as the second-instance evidence,
  each naming the ticket and the finding.** They are the bulleted entries in
  the ticket's Context, unchanged from the raise. A fifth, judged in class, is
  added as the paragraph that follows them. The enumeration, rather than a
  count of it, is read from
  `grep -n '^- \*\*OMN\|^\*\*A fifth instance' docs/tickets/active/EM-024-a-count-in-prose-has-no-falsifier.md`
  at `91798f3`, which returns:

  ```
  27:- **OMN-024, finding R4.2.** A boolean's count read "seven" where it is nine
  33:- **OMN-022-002, finding R7.4.** A finding line said "18 sites" where the file
  38:- **OMN-022-003, finding R7.3.** A Risks paragraph asserted a cost "beyond the
  42:- **OMN-020-001.** An acceptance-criterion note said "seven tests are
  62:**A fifth instance, surfaced after this ticket was raised, and judged in
  ```

  This description states no count of them, and neither does the new section.
  The list is their one site, which is what the section asks; a reader derives
  the number from the lines above. Which of the citations can be reproduced
  from a tree, and which are names a reader cannot open, is under Risks.
  *What a reader does differently:* a reader judges whether the second-instance
  bar was cleared by reading the instances, instead of taking the ticket's word
  for a number.

- [x] **AC4: the answer says what happens to a count duplicated across sites,
  and what instrument settles a count whose subject includes the sentence
  stating it.** Two paragraphs of the new section, in those terms.
  Duplication: "One site, and every other mention names the site rather than
  the number", with OMN-024's four sites named and the note that the repairing
  round re-created the claim it was repairing; under the section a number found
  in a second place is a defect on its face, visible without measuring
  anything. Self-reference: "Where the count's subject includes the sentence
  stating it, the instrument excludes prose", stating that a text search
  returns the sentence, that restricting the search to source paths does not
  fix it because a docstring is under `src/` too, and that a parser settles it
  because to a parser a docstring is a string constant and never a call.
  *What a contributor does differently:* a contributor with a count writes it
  once and points at it, and repairs it in one place rather than three; a
  contributor with a claim of absence over its own tree reaches for a parser
  first, instead of spending the three rounds OMN-024 spent.

- [x] **AC5: no existing rule is silently widened; a replacement is recorded as
  such.** §6's measured-number bullet is **extended, not replaced**. The added
  text says so in the bullet itself — "carries a further obligation, which
  extends this bullet and does not replace it ... This bullet is unchanged and
  still reaches every measured number, counts included." The diff shows no
  deletion in §6: `git diff 8abf61a..19cbb74 -- docs/ai-contributor-policy.md`
  reports 11 changed lines, of which the two deletions are the map row and the
  bullet line the insertion re-flows, and `git diff --stat 8abf61a..19cbb74 --
  docs/ai-contributor-policy.md` is the command. Nothing else in `docs/` is
  narrowed or widened: the new section states its own scope limits in "What
  this section does not reach", which defers the question of which numbers are
  measured at all back to §6 rather than re-deciding it.
  *What a reader does differently:* a reader of §6 who has read it before finds
  the bullet they remember, plus a sentence telling them what was added and
  that the old obligation is undiminished.

### Measured figures, each with its command
Every command below was run at `19cbb74`, the last commit that changes what any
of them counts, against the baseline `8abf61a`, this branch's point off `main`.
The two commits after it — the tier raise and its typo fix — and this
description's own commit touch only the ticket file and the board, which none
of these figures counts.

| Figure | Command | Result |
|---|---|---|
| quality gates, words before | `git show 8abf61a:docs/quality-gates.md \| wc -w` | 2229 |
| quality gates, words after | `git show 19cbb74:docs/quality-gates.md \| wc -w` | 3153 |
| policy, words before | `git show 8abf61a:docs/ai-contributor-policy.md \| wc -w` | 3266 |
| policy, words after | `git show 19cbb74:docs/ai-contributor-policy.md \| wc -w` | 3357 |
| PR template, words before | `git show 8abf61a:templates/PR-DESCRIPTION.md \| wc -w` | 876 |
| PR template, words after | `git show 19cbb74:templates/PR-DESCRIPTION.md \| wc -w` | 931 |
| README, words before | `git show 8abf61a:README.md \| wc -w` | 1044 |
| README, words after | `git show 19cbb74:README.md \| wc -w` | 1052 |
| rule-bearing files changed | `git diff --stat 8abf61a..19cbb74 -- README.md docs/ai-contributor-policy.md docs/quality-gates.md templates/PR-DESCRIPTION.md \| tail -1` | 4 files changed, 95 insertions(+), 5 deletions(-) |

The rule costs this repository 1,078 words across four documents, by
subtraction from the rows above and asserted nowhere else.

`EM-024`, `§6`, `AC3`, `8abf61a`, `19cbb74`, `91798f3` and the line numbers in
the AC3 block name things or locate them rather than measure a population, and
are outside §6's measured-number bullet by the test that bullet states.

### The gate this repository has
**It has none, and this section says so rather than implying a check that does
not exist.** The four machine gates in `docs/quality-gates.md` are the process
this repository publishes for adopting projects; this repository ships Markdown
and has no runner for any of them. At `91798f3`:

| Question | Command | Result |
|---|---|---|
| Python sources? | `git ls-files \| grep -Ec '\.py$'` | 0 |
| Any script or config a gate could run? | `git ls-files \| grep -Eic '\.(ya?ml\|toml\|sh\|cfg\|ini)$\|(^\|/)(Makefile\|justfile\|\.pre-commit-config\.yaml)$'` | 0 |
| CI configuration? | `git ls-files \| grep -c '^\.github/'` | 0 |
| What is tracked at the top level? | `git ls-files \| cut -d/ -f1 \| sort -u` | `.gitignore`, `DISCLOSURE.md`, `LICENSE`, `README.md`, `case-studies`, `docs`, `examples`, `templates` |

There is no `scripts/` directory. `ruff`, `mypy` and `pytest` have nothing here
to run against, and reporting them as passed would be false.

The one mechanical check this repository does have is the directory/status
invariant, and it was run. The command, at `91798f3`:

```sh
for f in docs/tickets/*/*.md; do
  d=$(basename $(dirname "$f"))
  s=$(grep -m1 '^status:' "$f" | sed 's/status: //')
  case "$d:$s" in
    ready:ready|active:in-progress|blocked:blocked|done:done) ;;
    *) echo "MISMATCH $f dir=$d status=$s" ;;
  esac
done
```

It printed nothing over the 41 ticket files that `ls docs/tickets/*/*.md | wc
-l` counts at that commit, which is the invariant holding. EM-024 is
`status: in-progress` in `docs/tickets/active/`, and EM-024-001 is
`status: ready` in `docs/tickets/ready/`.

### Falsification
N/A — this change makes no behavioural claim, and there is no suite. What a
reader or contributor does differently is stated per acceptance criterion
above, which is the form `templates/PR-DESCRIPTION.md` gives for a change with
no behavioural claim.

No review finding has been repaired, because no review has run; the class form
policy §6 asks for applies from the first round onward.

### Out of scope (per ticket)
Confirmed, one line each:

- **The four control-plane tickets themselves.** None was opened for editing;
  the control-plane repository was read only, to reproduce two citations.
- **Any general rule about duplicated prose.** The new section refuses this in
  terms: two sentences saying the same thing are a matter of style until one of
  them is a number about the tree. §5's bar on speculative abstraction is the
  reason, and the section's "What this section does not reach" paragraph is
  where the line is drawn for a later reader.
- **Retrospectively auditing every number in either project's records.** None
  was audited. One instance in this repository was found while reading the
  document the new section binds, and was raised as EM-024-001 under §4 rather
  than fixed here; that ticket is explicitly not a sweep and says so.

Also confirmed: the rule was not made a review obligation. The maintainer's
answer chose the structural option over that one, and `docs/tier-review-model.md`,
"What a review reports", is untouched — `git diff --stat 8abf61a..HEAD --
docs/tier-review-model.md` reports no change.

### How to verify
1. Read `docs/quality-gates.md`, "A count that describes the tree lives in a
   test", in full — it is one section and states its own scope, its degraded
   form and its falsifier.
2. `git diff 8abf61a..19cbb74 -- docs/ai-contributor-policy.md` — check that
   §6's bullet is extended and nothing in it is deleted, and that the map row
   for the quality gates now sends the question "where does a count that
   describes the tree live?" to the right document.
3. `git diff 8abf61a..19cbb74 -- README.md templates/PR-DESCRIPTION.md` — the
   index line and the two places in the template that already pointed at §6.
4. Re-run every command in "Measured figures" and in "The gate this repository
   has". They are the only numbers here.
5. `git show 91e14c2:docs/tickets/README.md | grep -n "Nothing is blocked"` and
   `... | grep -n "OMN-022-003 | blocked"`, in the control-plane repository, for
   the fifth instance's two sites in one file.
6. Check that this description restates no count that has a list: the instances
   are enumerated and never totalled, which is the section applied to itself.

### Risks / follow-ups
- **The degraded form is genuinely weaker, and this repository lives in it.**
  With no suite, a count's one site is a command in a document, which runs when
  a reader chooses to run it. Nothing goes red here. The section says so rather
  than hiding it, but a reader should not read "lives in a test" as something
  this repository can do.
- **Three of the five citations could not be reproduced from a tree.** In the
  control-plane clone available while working this ticket, `main` at `a1d16ff`
  holds OMN-024, OMN-022-002, OMN-022-003 and OMN-020-001 in `ready/`, and
  `git grep -n -E "R4\.2|R7\.4|R7\.3" <branch> -- docs/tickets` over the three
  ticket branches returns nothing: those review records live where the reviews
  ran and have not landed. The second-instance bar permits this — "a name a
  reader cannot open is still a name, quoted with its round" — and the citations
  are quoted with their rounds. What *is* reproducible is recorded: the fifth
  instance's two sites by the commands in Context, and OMN-022-002's 17 by
  `git grep -c "cause=" 5e89931 -- src/omnissiah/dispatch/transitions.py`.
  A reviewer weighing whether the bar was cleared should know which is which.
- **EM-015 is an adjacent instance that this section deliberately does not
  reach.** The README's two commit counts for one project are figures about a
  private project's history that no command in this repository can produce.
  They are §6's, not this section's, and were left out of the evidence rather
  than added because they were available. The scope test is the one the section
  states: does a command over *this* tree settle the number.
- **EM-024-001 raised**, under §4, for the one instance found in this
  repository while working: `docs/tier-review-model.md` states "eight" beside
  the list of the same eight and "thirteen" with no site at all. It is scoped
  to that sentence and does not decide whether a sweep is worth doing.
- **The falsifier's population is a default and is unmeasured.** Fifty closed
  tickets on an adopting project is a figure this project has no evidence for,
  named as a default for the reason the batch cap's ten-and-seven are, and the
  first adopting project replaces it.
- **The tier was raised, not lowered.** If a reviewer judges that a rule added
  inside an existing document is not clause 5, only the reviewer may lower it,
  recording the reasoning. EM-007-002 owns the underlying question and is
  blocked.

### Review
No round has run. The executor does not review its own work, and this ticket
remains `in-progress` in `active/` pending an independent pass under ADR-0002.

| Round | Must-fix | Where (rules / lists / documents / tests) | Inside previous round's fix | Repaired by |
|---|---|---|---|---|
| — | — | — | — | — |
