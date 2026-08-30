---
id: PRJ-161
title: Package runtime + ai in the wheel so a built artifact exposes runtime.api
status: done
tier: trivial
phase: 8
complexity: S
dependencies: [PRJ-159]
claimed_by: agent-str-161
claimed_at: 2026-08-20
blocked_at:
closed_at: 2026-08-20
---

# PRJ-161 — Package `runtime` + `ai` in the wheel

## Context

Surfaced by PRJ-159 (FastAPI adapter). `pyproject.toml` declares
`packages = ["core", "content"]`, so `runtime` and `ai` are **not** in the built
wheel — `pip install the-engine[serve]` yields `core`/`content` but **not**
`runtime.api` (or the harness/intents). Tests run from source, so CI never
noticed; but the **separate client repo (ADR-0011) that consumes a built
artifact** needs `runtime.api` importable. This closes that gap.

## Specification
- Add `runtime` and `ai` to the packaged modules in `pyproject.toml`
  (`packages = ["core", "content", "runtime", "ai"]`, or the equivalent
  `[tool.setuptools.packages.find]` include — match the existing declaration
  style).
- Confirm a build exposes them: `python -m build` (or the repo's build path) →
  the wheel contains `runtime/` (incl. `api.py`) and `ai/`; a fresh venv
  `pip install`-ing the wheel with the `serve` extra can `import runtime.api`.
- No code change — packaging metadata only.

## Acceptance criteria
1. `pyproject.toml` packages `runtime` + `ai` alongside `core`/`content`.
2. A built wheel exposes `runtime.api` (and `ai.harness`) — verified by a build +
   import check documented in the PR (a test is optional; a documented manual
   check is acceptable for packaging metadata).
3. `bash ci/run-checks.sh` exits 0 (unchanged behaviour — source tests are
   unaffected); 0 xfailed.

## Out of scope
- Publishing/distribution, versioning the package, or a release pipeline.
- Any `core`/`content`/`runtime`/`ai` code change.

## References
- `pyproject.toml` (the `packages` declaration), PRJ-159 (which flagged this),
  ADR-0011 (the separate client repo consumes the built contract).

## PR Description

### Ticket
PRJ-161 — Package `runtime` + `ai` in the wheel so a built artifact exposes `runtime.api`.

### Tier
trivial (packaging metadata only; no source, no schema, no CI-config change).

### Summary
`[tool.hatch.build.targets.wheel].packages` listed only `core`/`content`, so a
built wheel omitted `runtime` and `ai`. Added both to the wheel target so a built
artifact exposes `runtime.api` and `ai.harness` for the separate client repo
(ADR-0011). One-line metadata change; no code touched.

### Acceptance criteria
- [x] AC1: `pyproject.toml` packages `runtime` + `ai` alongside `core`/`content`
  — `packages = ["core", "content", "runtime", "ai"]` at `[tool.hatch.build.targets.wheel]`.
- [x] AC2: A built wheel exposes `runtime.api` (and `ai.harness`) — verified by
  build + import check (see How to verify). The `pip wheel` artifact contains
  top-level `ai`, `content`, `core`, `runtime`, including `runtime/api.py` and
  `ai/harness.py`; a clean venv `pip install the-engine-0.0.1-py3-none-any.whl[serve]`
  then imported both from `site-packages` (not source).
- [x] AC3: `bash ci/run-checks.sh` exits 0 (unchanged behaviour); 0 xfailed —
  ran it: `4414 passed, 2 warnings in 90.67s`, `all checks passed`, exit 0.
  (The 2 warnings are the environmental pytest-cache access-denied notices on
  the network share, not test failures.)

### Out of scope (per ticket)
No publishing/versioning/release-pipeline work; no `core`/`content`/`runtime`/`ai`
source change; `ai/intents/` untouched (PRJ-156 owns it). Confirmed the only
edited source file is `pyproject.toml`.

### How to verify
1. Build a wheel (build isolation fetches hatchling):
   `python -m pip wheel . --no-deps -w <dir>`
2. Inspect it:
   `python -c "import zipfile; z=zipfile.ZipFile('<dir>/the-engine-0.0.1-py3-none-any.whl'); import sys; print('runtime/api.py' in z.namelist(), 'ai/harness.py' in z.namelist())"`
   → `True True`.
3. Clean-venv install + import:
   `python -m venv v && v/Scripts/python -m pip install "<wheel>[serve]" && v/Scripts/python -c "import runtime.api, ai.harness; print(runtime.api.__file__)"`
   → resolves from `site-packages/runtime/api.py`.
4. `bash ci/run-checks.sh` → exits 0.

### Risks / follow-ups
None. Packaging metadata only; source tests run from the tree and are unaffected.
The `serve` extra (fastapi/uvicorn) remains optional per PRJ-159.
