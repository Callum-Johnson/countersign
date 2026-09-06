# Quality gates

What must pass before anything merges, at every tier.

```sh
ruff check .            # lint
ruff format --check .   # formatting, not negotiable, not hand-applied
mypy --strict           # strict type checking across all source packages
pytest --cov            # tests with coverage reporting
```

Contributors run these locally before opening a pull request. CI runs the
identical script afterwards. Failures block the merge regardless of tier.

There is a fifth gate that no tool runs. The falsification gate, below, is an
executor obligation discharged before the pull request is reported. It is
listed here because it is a condition of merge like the other four, and
because the four above cannot do its job.

**Retired when:** a gate is shown, over a stated count of pull requests, to
block merges that a reviewer passes without any change to the work — a
formatter fighting generated code, a type checker needing suppressions on most
files. That gate then costs review time and catches nothing; each gate below
carries its own line.

## The identical-script rule

The local command and the CI job are the same shell script in the repository,
not two configurations that resemble each other. Anything else produces the
"passes locally, fails in CI" conversation, which with an AI contributor
becomes an expensive loop: the agent cannot see CI, so it guesses, and it
guesses confidently.

**Retired when:** local and CI environments differ in a way one script cannot
express, and the "passes locally, fails in CI" loop is shown absent over a
stated population anyway.

**The script must not mutate state outside the working tree.** The ordinary
Python arrangement fails this: a gate script whose first step installs the
package in editable mode repoints the interpreter's import path at *this*
tree, for every process on the machine that shares that interpreter. With
several agents in parallel worktrees, one agent running the gate makes every
other agent's suite import the first agent's code. On the source project —
the rules engine in
[the growth case study](../case-studies/00-growth-2024-2026.md), which is
what "the source project" means throughout this document — three agents
independently deduced this and refused to run the script as written;
the gates were trustworthy only because each pinned its interpreter by hand
and printed the path as evidence. A script that is identical everywhere but
leaks across trees is identical in the wrong way. Install into an environment
the worktree owns, or run against the source tree without installing.

**Retired when:** the project runs one agent per machine by construction, so
that no process shares an interpreter with another tree.

## Review isolation

The identical-script rule's no-mutation constraint, one level up: a review
must not mutate the tree it reviews.

The falsification gate hands a reviewer a count to verify, and verifying it
looks like mutation — apply the wrong implementation, run the suite, count.
The gate is right to ask for that. Where it happens is the question. **Review,
including any mutation the gate asks for, runs in a worktree the reviewer
creates, owns and removes. The tree under review is read by the reviewer,
never written.** A review that writes nothing — a hosted reviewer reading a
diff — is not refused by this rule; what such a review cannot do is discharge
the run-the-suite duty, and that refusal is the tier model's. A reviewer that
cannot create a worktree at all — an agent handed a path and nothing else —
cannot discharge this rule; the review is then unavailable in ADR-0002's
sense, and the ticket says so rather than letting the review write in place.

**The tree is checked after the review returns**, before any repair or
further round: the status command reports nothing untracked and nothing
modified, and the worktree list shows only the worktrees the executor
created — a clone or a copy elsewhere is not the tree under review and is
not refused. Anything found is a finding against the review, recorded as
its own line after the round's row in the record, outside the must-fix
count and the two columns, and removed before the tree is used again, the
closing commit included.

The mechanism this guards against, stated so the class is understood and not
only the file: an interpreter that imports a module of a fixed name at start-
up, from any directory on its path, will run whatever a file of that name
contains before the test runner or the type checker examines anything. A copy
that exits zero under those tools makes both gates pass having examined
nothing, and only a gate that reads files as text — lint — sees it. In CPython
the module is `sitecustomize`; which invocations reach a root-level copy
depends on the invocation, and the source project's own record is the
authority on that. On OMN-021 on the control-plane project, one reviewer left
such a file at the root of the tree under review, in round 12 as that
project's policy-module comment records, and the lint gate was what failed;
another, in round 13, left a registered worktree the main tree's status
command does not show. The executor found both, by checking status and the
worktree list before every gate run as a private discipline. That discipline
is this rule.

It is the executor's check and not the reviewer's promise because the
party that will be blamed for a finding is the party that must be able to
show the tree was its own. A record that cannot say whether a finding was
in the work or in the review of it has lost the thing a review record is
for.

**Retired when:** review is dispatched by a mechanism that cannot write to
the tree under review — a hosted reviewer with a read-only checkout and its
own environment — and the project has no other reviewer; the post-review
check then checks nothing, and the worktree rule constrains nobody.

## Coverage: no regression, not a threshold

There is no global coverage percentage to hit. The rule is **no regression on
files you changed**. If a file sat at 92% before your change and 89% after,
that blocks — restore it, or raise a follow-up ticket and justify the deferral
in the pull-request body.

A fixed threshold is easy to satisfy badly. A project at "80% minimum" with a
well-covered core and an untested periphery reports the same number as one
with the reverse, and a contributor adding untested code to an
already-well-covered file can stay above the line. Measuring the delta on
changed files asks the only question that matters: did *this change* come with
its tests?

**Retired when:** every change records a red count under the falsification
gate, over a stated population, at which point coverage adds nothing the count
does not say more precisely.

## Coverage measures execution, not discrimination

The rule above asks whether a change came with tests. It cannot ask whether
the tests would notice if the change were wrong. Coverage records that a line
ran; it does not record that any assertion depended on what the line did. A
test that executes a changed line and would pass under the old implementation
as well as the new one satisfies the coverage rule and pins nothing.

A fully covered file can be fully unpinned. On one ten-ticket wave of the
source project, four separate changes passed the no-regression rule, one of
them on a file at 100% of statements and branches, while shipping tests that
could not fail: reverting
the exact line each change had fixed left the whole suite green. The mechanism
was ordinary each time. A predicate ended in an inclusive comparison, so the
old and new implementations agreed at both values the tests used and differed
only in a band between them, and no test sat in the band. In another case two
readings of a specification coincided on every fixture in the repository,
which made them the same function as far as the suite could tell, so no single
test case could have separated them however carefully it was written.

No machine gate in this document catches that. Every instance was caught by
independent review, and only because a reviewer changed the code and counted.
The gate that follows moves the count to where it is cheapest: before the
report, by the executor.

*Not a rule.* This section describes what coverage measures; it carries no
falsifier because it constrains nothing.

## The falsification gate

For each behavioural claim a change makes, the executor:

1. **Names the counterfactual** — a plausible wrong implementation the change
   rules out. Not a syntax error; the neighbour a competent contributor could
   have written. The other side of an inclusive comparison. The other reading
   of the specification. The fix one branch too shallow.
2. **Applies it and runs the suite.**
3. **Records the count** of tests that go red, beside the claim, in the
   pull-request description's Falsification section.

**A count of zero means the test is decorative and the claim is unpinned.**
The change may still be correct. The suite cannot tell, and neither can a
reviewer reading it, and a zero written down is a fact a reviewer can act on
where a zero omitted is not.

Two cases the obvious arrangement does not cover:

- **No arrangement discriminates.** Some tests cannot be made to fail against
  any plausible wrong implementation: the change is a refactor, or the
  discriminating input does not exist in the fixture set. Keep the test, and
  **label it in its own docstring as non-discriminating**, naming what it
  would take. Deleting it loses a regression check still worth having. Leaving
  it unlabelled beside a real pin is how unpinned claims shipped in the first
  place: the label is what lets a reviewer tell the two apart.
- **More than one rival.** Two candidate readings that coincide on every
  existing fixture are indistinguishable to the suite, and one new case
  cannot separate three readings. The gate needs one discriminating case per
  rival, each with its own count.

The gate is an executor obligation, not a reviewer checklist item, and the
distinction is the point. On the source project every instance was found at
review, and each cost a full review round of rework. Putting the count in the
report means the reviewer verifies a number rather than derives one.

**Retired when:** over a stated population of changes every recorded red count
is non-zero and no reviewer's mutation has found an unpinned claim the
executor's count missed. The gate then costs a suite run per claim and catches
nothing review would not.

**A test pins a claim, not a mechanism.** A test that asserts a helper was
called, or that a case is absent from a list, defends the executor's belief
about how the code works, and turns red when the belief is corrected rather
than when a caller is let down. The assertion names what the change guarantees
to a caller; the docstring names the claim. The example, from OMN-021 on the
control-plane project, in the commit its round 11 records: a test asserting
that a directory name matched nothing on a list, with a comment explaining why
the absence was correct, on a list whose purpose was to match it — a test
written to defend a defect. Such a test passes the coverage rule and passes
this gate as stated, because the wrong implementation it rules out is real.
What it fails is the gate's purpose, which is that a red test means a claim
was violated. The gate's companion for the repair of a review finding — name
the class, falsify per sibling — is stated with the executor's other duties in
the contributor policy's §6 and not restated here.

**Retired when:** over a stated population of tests that predate this rule
or that review let through, those that assert a mechanism are shown to have
caught regressions that claim-level tests missed more often than they have
blocked a correct change to the mechanism.

## Formatting is machine-applied

The formatter is authoritative and its output is not hand-adjusted. This is
worth stating explicitly in a repository with AI contributors, because an
agent asked to match surrounding style will otherwise produce a plausible
approximation of it, and review time gets spent on whitespace instead of
behaviour.

**Retired when:** the formatter's output is contested at review more often
than it is accepted, over a stated population of pull requests.

## Strict typing

Type hints are mandatory on every function signature, including private
functions and return types, and `--strict` must pass.

The value is sharpest with generated code. An agent that has misunderstood a
data shape produces code that reads fluently and fails the type checker
immediately. Without it the same misunderstanding survives review and surfaces
later as a runtime error in an unrelated place.

**Retired when:** the project's language or its generated code cannot satisfy
`--strict` without suppressions on most files, counted.

## Hooks may not be skipped

Skipping pre-commit hooks is on the forbidden-actions list. If a hook fails,
the cause gets fixed.

The rule exists because `--no-verify` is exactly the kind of locally
reasonable shortcut an agent will take to satisfy its immediate instruction,
and it defeats every gate above at once.

*Falsifier:* stated once, with the rule in the contributor policy's forbidden
actions, and not restated here.
