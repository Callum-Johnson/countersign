### PR description (required)

The PR description lives **inside the ticket file**, appended as a
`## PR Description` section at the bottom of the ticket before it is
moved from `active/` to `done/`. This keeps the review trail with the
ticket forever, makes it grep-friendly
(`grep -A 50 "PR Description" docs/tickets/done/PRJ-XXX-*.md`), and
eliminates the merge-conflict pattern that a shared root-level
`PR.md` file produced when branches landed in parallel.

A `PR.md` at the worktree root is **allowed as a working draft** while
the ticket is in flight — it is gitignored and must not be committed.
The final version goes into the ticket file before close.

Use this template. It is a markdown section that gets appended to the
ticket file, not a standalone file. Empty sections are not acceptable
— write `N/A` explicitly if a section truly does not apply.

```markdown
## PR Description

### Ticket
PRJ-XXX — <ticket title> (also in frontmatter; can be terse)

### Tier
<trivial | standard | critical> (also in frontmatter)

### Summary
<1-3 sentences. What does this change accomplish?>

### Acceptance criteria
Copy each AC from the ticket and tick it with evidence:
- [x] AC1: <criterion> — see `tests/unit/test_modifiers.py::test_caps_sv`
- [x] AC2: <criterion> — see implementation in `core/modifiers.py:42`
- [ ] AC3: <not done — explain why>

### Out of scope (per ticket)
Confirm nothing in this PR exceeds the ticket's scope:
- <list anything notable that was tempting but deferred>

### How to verify
Steps a reviewer or future agent can take to confirm this works:
1. `pytest tests/unit/test_modifiers.py`
2. `python -c "from core.modifiers import resolve; ..."`

### Risks / follow-ups
<known limitations, things to watch, follow-up tickets created>
```

### Definition of Done (all tiers)

A PR may not be merged unless all are true:

1. **All ticket acceptance criteria are met** (or explicitly deferred
   with rationale in the PR body).
2. **Tests added** for new behaviour. Tests use seeded dice for any
   randomness.
3. **`pytest`** passes cleanly. Zero failing, zero errored.
4. **`ruff check .`** clean.
5. **`ruff format --check .`** clean.
6. **`mypy --strict`** clean on changed packages.
7. **Coverage** on changed files is ≥ the prior baseline (no regression).
8. **No TODO / FIXME / XXX** introduced unless paired with a follow-up
   ticket ID in the comment, e.g. `# TODO(PRJ-042): handle ...`.
9. **PR description** is complete per the template above.
10. **No forbidden actions** taken (see AGENTS.md).

