---
id: EM-009
title: A review finding is repaired at its class, and the repair is falsified per sibling
status: ready
tier: critical
complexity: S
dependencies: [EM-006]
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

> Leave this section empty when authoring the ticket.
