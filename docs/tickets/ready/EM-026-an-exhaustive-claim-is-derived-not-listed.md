---
id: EM-026
title: An exhaustive claim is derived, not listed
status: ready
tier: standard
complexity: S
dependencies: []
claimed_by:
claimed_at:
closed_at:
---

# EM-026 — An exhaustive claim is derived, not listed

## Context

The falsification gate asks for a red count per claim and says a zero means
the test is decorative. It does not cover the case where the count is
**non-zero and the claim is still unpinned**, because the check and the
property are joined by a list the author wrote.

Four instances on OMNISSIAH, in four tickets, each found by a different
reviewer, between 2026-09-08 and 2026-09-15. In every one the suite was green,
the falsification count was recorded, and the property the test named was
absent.

| Ticket | The check | What the list missed |
|---|---|---|
| OMN-024, round 4 | `test_nothing_in_src_constructs_a_gate_runner` | population taken from calls whose `func` is a bare `ast.Name`; an **attributed** call escapes |
| OMN-034, AC5 | one helper guard plus two AST sweeps, certifying that no test starts a real agent | the reviewer used `subprocess.run` with a program name built as `"cla" + "ude"`, reached the host's real `claude.EXE` **while the certifying test stayed green** |
| OMN-020-002 | `test_every_spawn_site_that_runs_chosen_code_builds_its_environment` | iterates a hardcoded two-module tuple and matches only `subprocess.Popen`; missed a third site using `subprocess.run`, which handed a child 92 environment variables including a secret |
| OMN-038, AC4 | `test_a_reviewer_named_as_its_own_subject_is_refused` | the rival reddens it, so the count is 1 — but the test calls the function directly with an id no caller can supply, so **the path it pins is unreachable** |

The third is the sharpest on authorship: the executor wrote the limitation
into the test's own docstring — *"The enumeration pins the declared set; it
cannot see a third spawn site written without consulting it"* — and asserted
the completeness claim in module text anyway, on a governance surface, inside
a signed diff.

The fourth is the sharpest on the gate: every signal was green. The test
passed, the rival reddened it, the count was recorded and non-zero, and the
property — that a reviewer cannot name itself as its own subject — did not
hold for any caller that exists.

**The remedy is already known**, because OMN-034's repair found it. The guard
moved from three source-shaped checks to `subprocess.Popen.__init__`, the one
place every subprocess in the process converges, with the allowlist
**measured from an instrumented run** rather than guessed — 12,813 `git`
spawns, 179 `python.exe`, 18 `taskkill`. What made it work was not more care
about the list. It was not having a list.

## Specification

One rule in `docs/quality-gates.md`, beside the falsification gate, since it
is that gate's uncovered case rather than a new obligation.

### Files

- `docs/quality-gates.md` — the rule, after "The falsification gate"

No other document is edited. If the rule cannot be stated without amending
`docs/tier-review-model.md` or `docs/ai-contributor-policy.md`, that is a
finding and it stops and asks.

### The rule to land

Its content, not its wording. Whoever claims this writes it.

**A test that asserts something of *every* member of a population must derive
that population from the thing it describes, not restate it.** Three tiers,
in order of preference, because the first is not always available:

1. **Assert at the convergence point.** Where every member must pass through
   one place, check there. A population that cannot be enumerated wrongly
   beats one enumerated carefully.
2. **Derive the population.** Walk the tree, read the registry, ask the
   module — do not list the files, the call shapes, or the spellings.
3. **Where neither is possible, the docstring says what the check cannot
   see**, and *that* statement is itself pinned — the shape the falsification
   gate already uses for a non-discriminating test.

And the clause the fourth instance adds: **a rival must redden a path a
caller can take.** A count earned only through an entry point no caller
reaches is a zero wearing a number, and the gate's existing sentence — "a zero
written down is a fact a reviewer can act on" — does not reach it, because
nothing was written down as zero.

### What this rule is not

- **Not a ban on structural tests.** All four instances are worth keeping.
  The rule is about what makes their claim true, not about deleting them.
- **Not a demand for exhaustive proof.** Tier 3 is a real answer, and stating
  a gap honestly is what OMN-020-002 did right about network enforcement
  while doing it wrong about spawn sites — in the same file, on the same day.
- **Not retrospective.** It binds checks written after it lands. Nothing
  sweeps the existing corpus for lists.

### Falsification

The gate's own obligation applies to this ticket, and the honest difficulty
is stated rather than discovered: **this is a prose rule in a documentation
repository, and there is no suite for a sentence to redden.** What can be
done and should be:

- The rule is applied to the four instances above and asked whether it would
  have caught each. **If it would not have caught one, that is recorded, not
  smoothed** — a rule that catches three of four is still worth landing and
  the fourth is what retires it.
- The wording is checked against the falsification gate for contradiction. If
  the two disagree about what a zero means, one of them is wrong and this
  ticket says which.

**Retired when:** over a stated population of reviews, a check written after
this rule is found to have derived its population and still missed a member —
the rule would then be asking for the wrong thing rather than for more care.
Or: no reviewer finds a written-down population over a stated population of
changes, at which point the rule is a restatement of practice and leaves.

## Acceptance criteria

1. AC1: the rule is in `docs/quality-gates.md`, stating the three tiers and
   the reachable-path clause.
2. AC2: it is applied to all four instances in Context, and the answer for
   each — would this rule have caught it — is recorded, including any "no".
3. AC3: `git diff main...<branch> --name-only` names `docs/quality-gates.md`
   and the ticket file and nothing else, with the command and the head.
4. AC4: the rule does not contradict "The falsification gate"; the check is
   named in the description rather than asserted.
5. AC5: `standard` per EM-007-002 — one independent pass, closes on it, and
   the executor may not raise the tier.

## Out of scope

- Any change to the falsification gate's own text. This sits beside it.
- Sweeping OMNISSIAH's existing tests. The four instances are evidence, not
  a work list; three already have their own repairs.
- The review-debt observation from 2026-09-14 — that a review which happened
  but cannot be recorded should be recorded as a debt. **One day, four
  instances, all in one project and all caused by one absent capability**
  (nothing could create a reviewer run). It does not meet the second-instance
  bar as a *methodology* finding and is deliberately left out; it is named
  here so a later reader knows it was considered and why it was not taken.

## References

- `docs/quality-gates.md`, "The falsification gate" — the rule this extends,
  and its existing treatment of a zero and of a non-discriminating test
- OMNISSIAH OMN-024, OMN-034, OMN-020-002, OMN-038 — the four instances
- OMNISSIAH `tests/conftest.py`, `SPAWNABLE` and the `subprocess.Popen.__init__`
  guard — the remedy that worked, and the measurement behind its allowlist
- EM-007-002 — process-document changes are `standard`, one pass

## Notes

Raised on 2026-09-15 at the maintainer's request, after a day on OMNISSIAH in
which the same shape was found three times. The fourth instance arrived while
this ticket was being drafted.

**Tier: `standard`**, per EM-007-002: a process-document change takes one
independent pass and closes on it, and the executor may not raise it.

**The 2026-09-10 moratorium is discharged.** The maintainer's direction then
was that EM-025 would be the last rule-about-records ticket **until the
product had run once**. OMNISSIAH dispatched a real agent against a throwaway
repository on 2026-09-14 and it completed; the mediated chain — dispatch,
refuse, review, close, merge — ran end to end the same day. This rule is also
about tests rather than about records, which is the kind the 2026-09-10
review found was earning its keep.

## PR Description

> Leave this section empty when authoring the ticket.
