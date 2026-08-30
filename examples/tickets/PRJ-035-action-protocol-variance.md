---
id: PRJ-035
title: Fix Action protocol variance so concrete actions type-check
status: done
tier: critical
phase: 2
complexity: S
dependencies: [PRJ-006, PRJ-033]
claimed_by: orchestrator
claimed_at: 2026-07-02
blocked_at:
closed_at: 2026-07-02
---

# PRJ-035 — Fix Action protocol variance

## Context

The `Action` protocol in `core/actions/types.py` declares `type: str`
as a settable attribute. Concrete action dataclasses (`MoveAction`,
`EndPhaseAction`, `SelectUnitToMoveAction`, ...) declare
`type: str = field(default="...", init=False)` — effectively a
read-only constant. Under `mypy --strict`, a read-only concrete
attribute is not considered compatible with a settable protocol
attribute, so passing a concrete action where an `Action` is expected
fails the type check.

PRJ-033 worked around this with a narrow, commented `cast(Action, ...)`
in `ai/intents`. That is a smell that will recur every time an
external caller hands a concrete action to `apply_action`. Fix it at
the protocol.

## Specification

### Files

- `core/actions/types.py` (or wherever the `Action` protocol lives).
- Any spot currently using `cast(Action, ...)` to work around this
  (at least `ai/intents/movement.py` from PRJ-033 — remove the cast
  once the protocol is fixed; coordinate: this ticket may touch `ai/`
  only to remove the now-unnecessary cast).

### Fix

Declare the protocol's `type` as a read-only property so a read-only
concrete attribute satisfies it:

```python
from typing import Protocol, runtime_checkable

@runtime_checkable
class Action(Protocol):
    @property
    def type(self) -> str: ...
```

A frozen dataclass field satisfies a read-only property in mypy's
structural typing. Verify that:
- All existing concrete actions still satisfy `isinstance(x, Action)`
  at runtime (runtime_checkable protocols check attribute presence,
  which a dataclass field provides).
- `apply_action(state, MoveAction(...))` type-checks without a cast.
- The `cast(Action, ...)` in `ai/intents` can be removed and mypy
  still passes.

## Acceptance criteria

1. `Action.type` is a read-only property in the protocol.
2. `apply_action` accepts every concrete action type without a
   `cast` under `mypy --strict`.
3. The PRJ-033 `cast(Action, ...)` workaround is removed and
   `mypy --strict core content ai` (or `mypy --strict ai` if
   PRJ-034 hasn't landed) is clean.
4. Runtime `isinstance(action, Action)` still holds for every
   concrete action — a test asserts this for each.
5. All existing tests pass; `bash ci/run-checks.sh` exit 0.

## Out of scope

- Changing concrete action shapes.
- Any behavioural change to dispatch.

## References

- PRJ-006 (Action protocol origin), PRJ-033 (surfaced the cast).
- docs/conventions.md §7.

## Notes

`tier: critical` because it changes a public engine API contract
(the `Action` protocol) that every action type and the dispatcher
depend on. Small change, but load-bearing.

If PRJ-034 (CI gating for `ai/`) has not yet landed when this is
worked, run `mypy --strict ai` manually to confirm the cast removal
is clean.

## PR Description

> Leave empty; implementing agent fills it in per CONTRIBUTING.md §3.

## PR Description

### Ticket
PRJ-035 — Fix Action protocol variance so concrete actions type-check.

### Tier
critical (changes the `Action` protocol, a public engine API contract
every action type and the dispatcher depend on).

### Summary
Changes `Action.type` from a settable protocol attribute to a read-only
property, so concrete actions (whose `type` is a frozen `init=False`
dataclass field — read-only) satisfy the protocol structurally under
`mypy --strict`. Removes the `cast(Action, ...)` workaround and its
now-unused `cast`/`Action` imports from `ai/intents/movement.py`.

### Acceptance criteria
- [x] AC1: `Action.type` is a read-only property — `core/actions/types.py`.
- [x] AC2: `apply_action` accepts concrete actions without a cast under
  `mypy --strict` — verified by `_accepts_action(action: Action)` helper
  in `tests/unit/test_actions.py` (mypy type-checks the assignment) and
  by `_validates` in `ai/intents/movement.py` now calling
  `apply_action(state, action)` directly.
- [x] AC3: PRJ-033 `cast` removed; `mypy --strict core content ai`
  clean ("Success: no issues found in 32 source files").
- [x] AC4: runtime `isinstance(action, Action)` holds for a read-only
  `type` field — `test_action_protocol_recognises_readonly_type_field`.
  Existing `test_action_protocol_recognises_dataclass_with_type_attribute`,
  `_rejects_object_without_type_attribute`, `_rejects_bare_object` all
  still pass.
- [x] AC5: all tests pass; `bash ci/run-checks.sh` exit 0 (985 passed).

### Out of scope (per ticket)
- No concrete action shape changes (kept `type: str = field(default=...,
  init=False)`).
- No dispatch behaviour change.

### How to verify
1. `mypy --strict core content ai` — clean, no cast needed.
2. `grep -rn cast ai/` — no results (workaround removed).
3. `bash ci/run-checks.sh` — exit 0.

### Risks / follow-ups
- `runtime_checkable` protocols only check attribute *presence*, so
  `isinstance(x, Action)` is unchanged in strictness — a plain object
  with any `type` attribute still passes `isinstance` (documented
  limitation of runtime_checkable, not introduced here).
- Implemented directly by the orchestrator during recovery after the
  wave-11 subagents hit the account session limit at launch (zero
  commits landed). Work is identical in scope to the ticket spec.
