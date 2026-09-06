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
