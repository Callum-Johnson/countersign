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

## The identical-script rule

The local command and the CI job are the same shell script in the repository,
not two configurations that resemble each other. Anything else produces the
"passes locally, fails in CI" conversation, which with an AI contributor
becomes an expensive loop: the agent cannot see CI, so it guesses, and it
guesses confidently.

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

## Formatting is machine-applied

The formatter is authoritative and its output is not hand-adjusted. This is
worth stating explicitly in a repository with AI contributors, because an
agent asked to match surrounding style will otherwise produce a plausible
approximation of it, and review time gets spent on whitespace instead of
behaviour.

## Strict typing

Type hints are mandatory on every function signature, including private
functions and return types, and `--strict` must pass.

The value is sharpest with generated code. An agent that has misunderstood a
data shape produces code that reads fluently and fails the type checker
immediately. Without it the same misunderstanding survives review and surfaces
later as a runtime error in an unrelated place.

## Hooks may not be skipped

Skipping pre-commit hooks is on the forbidden-actions list. If a hook fails,
the cause gets fixed.

The rule exists because `--no-verify` is exactly the kind of locally
reasonable shortcut an agent will take to satisfy its immediate instruction,
and it defeats every gate above at once.
