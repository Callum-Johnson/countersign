---
id: PRJ-001
title: Repo skeleton, tooling, and CI config
status: done
tier: critical
phase: 1
complexity: M
dependencies: []
claimed_by: agent-str-001
claimed_at: 2026-06-30
closed_at: 2026-06-30
---

# PRJ-001 — Repo skeleton, tooling, and CI config

## Context

The repo currently contains only documentation. This ticket
establishes the Python project skeleton, tooling configuration, and
the directory layout that all subsequent tickets build on. Locks in
the conventions referenced by `docs/conventions.md`.

## Specification

### Files

- `pyproject.toml` — project metadata, dependencies, tool config.
- `core/__init__.py` — empty.
- `content/__init__.py` — empty.
- `tests/__init__.py` — empty.
- `tests/unit/__init__.py` — empty.
- `tests/integration/__init__.py` — empty.
- `tests/scenarios/__init__.py` — empty.
- `tests/fixtures/__init__.py` — empty.
- `tests/conftest.py` — empty for now (fixtures land later).
- `.pre-commit-config.yaml` — ruff + mypy hooks.
- `.python-version` — `3.12`.
- `ci/run-checks.sh` — POSIX shell script that runs the CI gate suite
  locally (ruff, mypy, pytest). Mirrors what CI would run.

### pyproject.toml contents

Required sections:

- `[project]` with `name = "the-engine"`, `requires-python = ">=3.12"`,
  initial version `0.0.1`.
- `[project.optional-dependencies]` with a `dev` extra containing
  ruff, mypy, pytest, pytest-cov, hypothesis.
- `[tool.ruff]` — line length 88, target Python 3.12, standard rule
  selection (E, F, I, B, UP, ANN, SIM, RUF) with sensible per-file
  ignores for tests.
- `[tool.ruff.format]` — defaults.
- `[tool.mypy]` — `strict = true`, `python_version = "3.12"`, packages
  `core` and `content` enforced; tests allowed slightly relaxed.
- `[tool.pytest.ini_options]` — `testpaths = ["tests"]`, useful
  defaults (verbose, show-locals on fail).
- `[tool.coverage.run]` — source = ["core", "content"], branch = true.

Runtime dependencies (Pydantic, msgspec, etc.) are added by later
tickets that need them. This ticket adds **dev tooling only**.

### Pre-commit hooks

`.pre-commit-config.yaml` runs:
- `ruff check --fix`
- `ruff format`
- `mypy --strict` (on staged files)

Document in the file how to install (`uv tool install pre-commit && pre-commit install`).

### ci/run-checks.sh

A single script that runs:
```sh
set -e
ruff check .
ruff format --check .
mypy --strict core content
pytest --cov=core --cov=content --cov-report=term-missing
```

Exit non-zero on any failure.

## Acceptance criteria

1. `pyproject.toml` validates: `python -m pip install -e .[dev]` runs
   without error.
2. `ruff check .` on the empty skeleton returns exit code 0.
3. `ruff format --check .` returns exit code 0.
4. `mypy --strict core content` returns exit code 0 (no files to
   check, but config loads cleanly).
5. `pytest` returns exit code 5 ("no tests collected") cleanly — not
   an error.
6. `bash ci/run-checks.sh` exits 0 (or 5 from pytest with no tests is
   acceptable; document this in the script).
7. The `.gitignore` (already in repo) is unchanged or only extended,
   not narrowed.
8. The `__init__.py` files are empty (no auto-imports).
9. `pre-commit install` works on a freshly cloned repo (without
   actually running hooks in CI — the config just needs to be valid).

## Out of scope

- Adding any runtime dependencies (Pydantic, msgspec, FastAPI). Done
  by later tickets when first needed.
- Writing any actual code in `core/` or `content/` — just `__init__.py`
  files.
- Setting up a GitHub Actions workflow file. The repo is local-only;
  the shell script in `ci/` is sufficient until a remote is added (per
  CONTRIBUTING.md §9).
- Configuring a release/publish workflow.

## References

- DESIGN.md §5 — Repository Structure (shows the target layout).
- CONTRIBUTING.md §5 — CI gates (defines what `ci/run-checks.sh` runs).
- docs/conventions.md §1 — Language and tooling (Python 3.12+, ruff,
  mypy, pytest, hypothesis).

## Notes

- Use `uv` if available for fast dependency resolution; otherwise
  standard `pip` is fine.
- Line length 88 matches Black's default and is what ruff uses by
  default if unspecified, but pin it explicitly so it cannot drift.
- Mypy strict mode is non-negotiable per conventions. Per-file
  relaxations are allowed via `[[tool.mypy.overrides]]` if a third-party
  library has no stubs — document each override with a comment.
