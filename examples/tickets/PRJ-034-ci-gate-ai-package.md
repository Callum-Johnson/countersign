---
id: PRJ-034
title: Gate the ai/ package in CI (mypy + coverage)
status: done
tier: standard
phase: 2
complexity: S
dependencies: [PRJ-033]
claimed_by: orchestrator
claimed_at: 2026-07-02
blocked_at:
closed_at: 2026-07-02
---

# PRJ-034 — Gate the ai/ package in CI

## Context

PRJ-033 added the `ai/` package (intent library). `ci/run-checks.sh`
and the mypy/coverage config in `pyproject.toml` only cover
`core content`, so `ai/` is not gated by CI — its type-safety and
coverage were verified manually during PRJ-033 but nothing prevents
a future regression. This ticket brings `ai/` under the standard CI
gates.

## Specification

### Files

- `ci/run-checks.sh`
- `pyproject.toml`

### Changes

1. **mypy**: extend the strict check to include `ai`:
   `mypy --strict core content ai`.
2. **coverage**: add `ai` to `[tool.coverage.run] source`.
3. **run-checks.sh**: update the pytest `--cov` invocation to include
   `--cov=ai`.
4. Confirm `ai/` currently passes: `mypy --strict ai` was clean at
   PRJ-033 close and coverage was 100%, so no `ai/` code changes
   should be needed. If a regression has crept in since, fix it or
   raise a blocker.

## Acceptance criteria

1. `ci/run-checks.sh` runs mypy over `core content ai` and coverage
   includes `ai`.
2. `pyproject.toml` coverage source includes `ai`.
3. `bash ci/run-checks.sh` exits 0 with `ai/` now gated.
4. No regression in overall pass rate.

## Out of scope

- Any change to `ai/` behaviour.
- Restructuring the CI script beyond adding `ai` to the existing
  gates.

## References

- PRJ-033 PR Description (flagged this as a follow-up).
- CONTRIBUTING.md §5 (CI gates).

## Notes

`tier: standard` because it touches CI config (which the tier rubric
lists under critical for CONTRIBUTING.md itself, but `ci/run-checks.sh`
and `pyproject.toml` tool config are ordinary config here). If the
implementer judges the CI-config change warrants critical review, they
may raise the tier.

## PR Description

> Leave empty; implementing agent fills it in per CONTRIBUTING.md §3.

## PR Description

### Ticket
PRJ-034 — Gate the ai/ package in CI (mypy + coverage).

### Tier
standard (CI/tool config only; no engine behaviour change).

### Summary
Brings the `ai/` package (PRJ-033 intent library) under the standard
CI gates: adds `ai` to mypy `files`, the `mypy --strict` invocation in
`ci/run-checks.sh`, the coverage `source`, and the pytest `--cov`
flags. Keeps CONTRIBUTING.md §5's documented commands in sync.

### Acceptance criteria
- [x] AC1: `ci/run-checks.sh` runs `mypy --strict core content ai` and
  pytest coverage includes `--cov=ai`.
- [x] AC2: `pyproject.toml` coverage `source` includes `ai` (and mypy
  `files` includes `ai`).
- [x] AC3: `bash ci/run-checks.sh` exits 0 with `ai/` gated — `ai/`
  modules now appear in the coverage report (`ai/intents/layout.py`,
  `ai/intents/movement.py` at 100%).
- [x] AC4: no regression — 985 passed, overall 99%.

### Out of scope (per ticket)
- No `ai/` behaviour or `core/` change.
- No `fail_under` threshold added (project uses no-regression per
  CONTRIBUTING.md §5).

### How to verify
1. `bash ci/run-checks.sh` — the mypy line reads `core content ai`; the
   coverage table lists `ai\intents\*`.
2. Exit 0.

### Risks / follow-ups
- Implemented directly by the orchestrator during recovery after the
  wave-11 subagents hit the account session limit at launch. `ai/` was
  already type-clean and 100%-covered from PRJ-033/PRJ-035, so gating it
  required no `ai/` code changes.
