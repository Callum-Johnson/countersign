---
id: EM-009
title: A review finding is repaired at its class, and the repair is falsified per sibling
status: done
tier: critical
complexity: S
dependencies: [EM-006]
claimed_by: claude-fable-5-1
claimed_at: 2026-09-06
closed_at: 2026-09-06
---

# EM-009 — A review finding is repaired at its class

## Context

EM-006 introduces the falsification gate: for each behavioural claim the
executor names the wrong implementation the change rules out, applies it, and
records the count of tests that go red. EM-006's Out of scope deferred a
neighbouring question in these words: "whether a defect recurring at many
sites should be enumerated as a class before being fixed instance by
instance", supported at that time by one project's evidence. This ticket is
that question, with a second project's evidence.

The evidence is OMN-021 on the control-plane project that implements this
process mechanically. Its Review section records, per round, how many of the
round's must-fixes were found inside the previous round's own repair — 1, 2, 3,
3, 2, 2, 2, 3, 4, 3, 0, 2, 2 for rounds 2 to 14 — which sums to 29 of the 46
must-fixes recorded in the same section. That is the shape of a loop repairing
instances: a fix is correct where the reviewer pointed and lands one branch too
shallow, one function too wide, or on one side of a two-sided question, and the
next round finds the sibling.

Three of the recorded repairs show the mechanism directly:

1. **Round 13's commit is titled "the shape covered one of four suffix
   families".** Round 12 had found that a root-level module shadows a gate
   tool; the repair matched `.py`. The class was "every suffix the interpreter
   imports", and the question that enumerates it — what does the interpreter
   load — was not asked until the next round asked it.
2. **Round 12's diagnosis** is recorded in its commit title: "the lists asked
   about config, never resolution". Five consecutive rounds had found one
   process list one entry short, because the list had only ever been built by
   asking which file a tool reads as configuration, and never how the shell or
   the interpreter finds the tool. The second question produces a different
   class with different members, and no number of answers to the first
   question reaches them.
3. **Round 11 found a test asserting that a hole was intended.** A test
   asserted that a particular directory name matched nothing on a list, with a
   comment explaining why that was correct. The premise was false. The test
   pinned the executor's belief about a mechanism rather than the claim the
   list exists to make, and would have turned red for anyone correcting the
   belief — a test written to defend a defect.

None of these is a failure of the falsification gate as EM-006 states it. Each
repair did name a wrong implementation and did count red tests. What the gate
does not ask is whether the wrong implementation named is one member of a
family, and whether the repair covers the family.

## Specification

Documentation changes only. Extends the falsification gate; changes nothing
in it.

### Files

- `docs/ai-contributor-policy.md` §6, the falsification gate as EM-006 lands
  it — a paragraph stating the class obligation for repairs of review
  findings.
- `templates/PR-DESCRIPTION.md`, `### Falsification` — the per-sibling form
  for review repairs.
- `docs/quality-gates.md`, the falsification gate section as EM-006 lands it —
  the mechanism-versus-claim rule for tests.

### Public surface

N/A — this repository publishes documents. The change adds an obligation to
an existing gate.

### Behaviour

- For each review finding the executor repairs, the pull-request description
  names **the class**: the question which, asked of the whole change,
  produces this finding and its siblings. "What does the interpreter load" is
  a class; "`.py` files at the root" is an instance.
- The description then names **the siblings** that question enumerates, and
  for each sibling the test that pins it and the count of tests that go red
  under the sibling's wrong implementation. One case per rival, as EM-006
  already states for readings that coincide on the fixtures.
- A repair that names no class is recorded as a repair of the instance, in
  those words. That is permitted — some findings are singular — but it is a
  statement the reviewer can check, and the next round finding a sibling is
  then a finding against the repair's own claim.
- A test pins **a claim, not a mechanism**. A test that asserts a helper is
  called, or that a case is absent from a list, defends the executor's belief
  about how the code works and turns red when the belief is corrected. The
  rule states the form: the assertion names what the change guarantees to a
  caller, and the docstring names the claim. Round 11's test is the example,
  in engineering terms — an assertion that a name matches nothing, with a
  comment justifying the absence, on a list whose purpose was to match it.

## What this refuses, and what it costs

> Added 2026-09-05 on review of the wave, applying EM-010's two questions to the ticket that proposes them. A figure measured here names its baseline in the same sentence; a figure from a private project names the ticket section it is taken from; an assumption says so. Raised alongside EM-014; corrected after independent review of c0111ae.

**Refuses.**

- A one-line fix for a finding the executor believes is singular, unless the
  pull-request description says "repair of the instance" in those words. The
  declaration is permitted. Its cost is that it becomes a claim the next round
  can hold against the executor, so executors will enumerate defensively —
  which is the rule working, and is also more enumeration than some findings
  deserve.
- Repairs whose class question has no finite answer. "What does the
  interpreter load" enumerates; "what could a user type" does not. The rule
  gives no exit for the unenumerable class, and an executor meeting one has
  to choose between an honest "repair of the instance" and an invented
  enumeration.

**Costs.**

- This ticket multiplies EM-006's cost by sibling count: per finding, one
  mutant-and-count per sibling. On OMN-021's 46 must-fixes, taken from its
  Review section as this ticket's Context quotes them, an assumed three
  siblings each would be about 138 suite runs, which at the twelve-minute
  figure EM-012 reports from OMN-025 is roughly twenty-eight hours of gate
  time on one ticket. The record gives rounds, not gate runs, so the figure
  that ticket actually paid is not available and is not asserted. The
  twenty-eight hours is an upper bound on an assumed sibling count; the first
  adopting project to work a ticket under the rule can replace the
  assumption, and this repository cannot.
- Adds an executor obligation to policy section 6, which carries five today,
  measured 2026-09-05 at 8b0a8b4.

## Acceptance criteria

1. AC1: `docs/ai-contributor-policy.md` states the class obligation as an
   executor obligation discharged in the repair of a review finding, with the
   instance-versus-class distinction given by example.
2. AC2: `templates/PR-DESCRIPTION.md`'s Falsification section carries the
   per-sibling form — class, siblings, test and red count per sibling — and
   the "repair of the instance" declaration for the singular case.
3. AC3: `docs/quality-gates.md` states the claim-not-mechanism rule for tests,
   with the asserted-absence example.
4. AC4: The three documents do not restate one another in full; each carries
   its part and references the others, consistent with EM-006's AC4.
5. AC5: The source ticket's figures, where quoted, name the section they are
   derived from in the same sentence.
6. AC6: Critical tier per ADR-0002: an independent agent that did not perform
   the work reviews this against the artifacts and records findings in the
   pull-request description.

## Out of scope

- The stopping rule that reads the repairs-of-repairs signal. EM-007.
- Any change to EM-006's gate for original work. This ticket concerns the
  repair of a finding, where the wrong implementation is known and the
  question is its family.
- Prescribing how a class is found. Round 12's method on the source ticket —
  ask the question the list was never built by — is one method and is given
  as an example, not a procedure.

## References

- EM-006 — the falsification gate this ticket extends, and its Out of scope,
  which named this question and deferred it.
- `docs/ai-contributor-policy.md` §6, `docs/quality-gates.md`,
  `templates/PR-DESCRIPTION.md` — as EM-006 lands them.
- OMN-021 on the control-plane project — its Review section for the
  per-round figures, and the commits its rounds 11, 12 and 13 record.

## Notes

**Dependency.** This ticket edits text EM-006 introduces, so it depends on
EM-006 and cannot start before it closes. If EM-006 is split along the line
its Notes suggest, this depends on the half that lands the gate.

**Why the mechanism rule lives with the gate and not with the tests
guidance.** A test pinning a mechanism passes the coverage rule and passes the
falsification gate as stated — the wrong implementation it rules out is real.
What it fails is the purpose of the gate, which is that a red test means a
claim was violated. It belongs beside the gate because it is the gate's
loophole.

**Working this with EM-007, EM-008, EM-010 and EM-011.** See EM-007's Notes.

## PR Description

### Ticket
EM-009 — A review finding is repaired at its class

### Tier
`critical` — process-surface change (clause 5): it adds an executor
obligation to the definition of done and a rule to the gates.

**Independent review obtained**, per ADR-0002: a separate agent, given the
ticket, the diff and the two questions, and not the executor's reasoning,
reviewed the change in two rounds, read-only. Findings are under
Review; the tree was checked clean after each round.

### Summary
Policy §6 gains the class obligation for the repair of a review finding,
with the instance-versus-class example and the "repair of the instance"
declaration; the template's Falsification section gains the per-sibling
form; the quality gates gain the claim-not-mechanism rule with the
asserted-absence example, beside the gate whose loophole it is. Both new
rules carry a Retired-when line, stated under ADR-0003's exemption clause,
which this description says so per that clause.

### Acceptance criteria
- [x] AC1: the class obligation as an executor duty with the example —
  `docs/ai-contributor-policy.md` §6, the bullet beginning "A review
  finding is repaired at its class", with "what does the interpreter load"
  against "`.py` files at the root".
- [x] AC2: the per-sibling form and the instance declaration —
  `templates/PR-DESCRIPTION.md`, Falsification, the paragraph and two lines
  after the claim lines.
- [x] AC3: the claim-not-mechanism rule with the asserted-absence example —
  `docs/quality-gates.md`, "The falsification gate", the paragraph
  beginning "**A test pins a claim, not a mechanism.**"
- [x] AC4: no restatement — the rule is stated in full once in the policy;
  the gates carry one pointer sentence to it; the template carries the form
  and a pointer; the policy points at the gates for the mechanism reasoning.
- [x] AC5: figures name their section — no OMN-021 figure is quoted; the
  one item taken from it, the round-11 test, names the ticket, the project
  and the commit its round records. Round 1 found it attributed to the wrong
  project and it was corrected.
- [x] AC6: independent review — see Review.

### Falsification
N/A — no behavioural claim. What a reader does differently, per criterion:
- AC1: an executor repairing a finding writes the class question and its
  siblings, or the words "repair of the instance", instead of a one-line
  fix.
- AC2: a closing executor has a line per repaired finding and the next
  reviewer a claim to check.
- AC3: an executor writes the assertion as what a caller is guaranteed;
  a reviewer with a non-zero red count still asks whether the test pins a
  claim.
- AC4, AC5: nothing beyond finding each rule and source once.

Repairs of this ticket's own review findings, in the form this ticket
lands. There is no suite; each sibling says what a reader does
differently.
- R1.1 — class: which documents define "the source project", and does each
  use of it in text this ticket adds match that definition? Siblings: the
  quality gates (defines it as the rules engine; the added use did not
  match — repaired, a reader now reaches the right project); the policy and
  the template (no use added). Red: a reader following the old attribution
  reached the wrong case study.
- R1.3 — class: which obligations this ticket adds have no discharge in a
  repository without a suite? Siblings: the per-sibling red count (repaired
  in the template: a sibling says what a reader does differently); the
  claim-level assertion rule (no discharge needed; it describes a test); the
  instance declaration (dischargeable as words). Red: an executor here could
  not have written this section honestly before the repair.
- R1.4, R1.5, R1.6, R1.8 — repair of the instance, each: a misplaced line,
  an unnamed population, a missing exit, an unindexed reference. Each is
  one sentence in one place and the round-1 record names no sibling.

### Out of scope (per ticket)
Confirmed: the stopping rule is unchanged in substance — the one edit to
`docs/tier-review-model.md` replaces "the class obligation EM-009 adds to
the falsification gate" with "the class obligation in the contributor
policy's §6", a cross-reference that is now true, and it is beyond the
ticket's Files list and declared here; EM-006's gate for original work is
untouched, both hunks in the gates document being insertions; no method for
finding a class is prescribed.

### Review
| Round | Must-fix | Where (rules / lists / documents / tests) | Inside previous round's fix | Repaired by |
|---|---|---|---|---|
| 1 | 2 (of 8 findings) | documents: the round-11 example attributed to the wrong project (must-fix); the per-sibling count undischargeable without a suite (must-fix); two Retired-when lines adjacent with nothing tying either to its rule; the mechanism falsifier's population unnamed; no exit for the unenumerable class; the obligation binding notes as well as must-fixes; the finding index unnumbered; the cross-reference edit beyond Files | — | 0d48410 |
| 2 | 0 (of 4 notes) | documents: two ragged lines from round-1 repairs; the policy named "the stopping rule" without saying where it is; the no-suite exit lived in the template only | 4 of 4 | the closing commit |

Derived total: 2 must-fix over two rounds.
- R1.1 · permits · the baseline rule (policy §6) · the example named "the
  source project", which the gates define as the rules engine, for a test
  on the control-plane project — remedy: name the ticket, the project and
  the commit; no tightening.
- R1.2 · permits · scope · the tier-model cross-reference exceeds Files —
  remedy: declare it; done above.
- R1.3 · refuses · the class obligation · the per-sibling red count has no
  discharge in a repository with no suite, and "repair of the instance"
  would be false for a finding with siblings — remedy: the template says
  what a sibling records where there is no suite; a loosening.
- R1.4 · refuses · the two new Retired-when lines · adjacent, unattributed
  — remedy: each now follows its rule.
- R1.5 · refuses · the mechanism rule's falsifier · population unnamed —
  remedy: tests that predate the rule or that review let through.
- R1.6 · refuses · the class obligation · no exit for a class with no
  finite enumeration — remedy: recorded as the stopping rule's third
  condition records a list; a loosening.
- R1.7 · refuses · the class obligation · it binds notes as well as
  must-fixes, and the ticket priced it on must-fixes; on this repository's
  four closed records at 0781e98 that is 55 findings against 5 must-fixes,
  per the reviewer's count of their Review tables — recorded, not fixed,
  since the Behaviour says "each review finding"; the maintainer may
  narrow it by a retirement ticket.
- R1.8 · refuses · the template · findings unindexed — remedy: n.k in both
  forms.
Round 2 found no must-fix; its four notes all sat inside round-1 remedies
and are taken at close: both paragraphs re-flowed, the policy names "When
review ends" and its document, and the no-suite exit is in the rule as well
as the form. Round 2 verified the attribution against the ticket's Context
and References and the n.k indexing across both forms.
Post-review tree check after each round: `git status --porcelain` empty,
`git worktree list` showing only the main tree.

### How to verify
1. `grep -n "repair of the instance" docs/ai-contributor-policy.md
   templates/PR-DESCRIPTION.md` — the declaration in both, the rule once.
2. `sed -n '/^## The falsification gate/,/^## Formatting/p'
   docs/quality-gates.md | grep -n "Retired when\|A test pins\|The gate is
   an"` — each Retired-when line follows its rule.
3. `git diff 301df38..HEAD -- docs/tier-review-model.md` — one
   cross-reference, nothing else.
4. `wc -w` at 301df38 and at close: policy 1,717 to 1,944; gates 1,436 to 1,672; template 709 to 799, as the reviewer measured at 0d48410, before the close commit's re-flow and one clause.

### Risks / follow-ups
- The obligation falls per finding, not per must-fix, and this repository's
  reviews return roughly eleven findings per must-fix. The ticket's cost
  section priced it on must-fixes. A project adopting this should expect
  the per-sibling form on most findings, and this repository's next closed
  records will show what that costs in words.
- The first discharge of the rule is this description's own Falsification
  section. It shows the form works for documentation findings and that
  "repair of the instance" is the honest answer more often than the rule's
  emphasis suggests.

