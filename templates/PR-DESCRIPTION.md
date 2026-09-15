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
Copy each AC from the ticket and tick it with evidence. Every measured
number names its baseline in the same sentence and is read from a command
the description names, run after the last commit that changes it
(contributor policy §6). A number that something other than its own sentence
determines names its one site — the test that measures it, or, where the
project has no suite, the command or the list — and is not restated anywhere
else in the description; where a list or a search would serve, no number is
written, and a number kept anyway says which determiner it copies and why
naming it would not serve the reader there (quality gates, "A number
determined elsewhere has one site that goes red"):
- [x] AC1: <criterion> — see `tests/unit/test_modifiers.py::test_caps_sv`
- [x] AC2: <criterion> — see implementation in `core/modifiers.py:42`
- [ ] AC3: <not done — explain why>

### Falsification
One line per behavioural claim: the wrong implementation ruled out, and the
count of tests that go red under it (see "The falsification gate" in the
quality-gates document). A zero is written as a zero. A test that cannot
discriminate is listed with its docstring label and what it would take.
A change with no behavioural claim writes `N/A` and says, per acceptance
criterion, what a reader would do differently because of it.
- <claim> — mutant: <what was changed>; red: <N> of <M> tests
- <claim> — non-discriminating: <label>; would need <input or fixture>

For each repair a line here is owed of, `<n>.<k>` as numbered in Review:
the class — the question that enumerates the finding and its siblings —
and each sibling with its test and red count; or the words `repair of
the instance` (contributor policy §6). A class the question does not
finitely enumerate — "what could a user type" — is the third form §6
gives, and is neither of the two above: the siblings are best-effort and
the line states the coverage, the way the third condition of "When review
ends" in `docs/tier-review-model.md` records a list. Where the change has
no suite, each sibling says what a reader would do differently, as the
line above says for a claim.

Which repairs owe a line is settled by the rules that ask for this form,
each of which says which repairs it asks it of. Read those rules rather
than a list of exceptions here: a list has to be scoped by hand every
time a rule is added, while a rule that wants the form asks for it by
asking. Two rules ask as this is written, and naming them is an
inventory, not the test. The contributor policy's §6 asks the form of a
repaired must-fix, and of the repair of a finding the reviewer left
unranked. The class signal in `docs/tier-review-model.md`, "What a
review reports", asks it of the round's repair of the rule the signal
fired on, whatever the two findings' ranks — that signal has a trigger
of its own, which §6's narrowing does not reach. So the repair of a
finding the reviewer ranked a note owes no line of its own: not by an
exception written here, but because §6 does not reach it and no other
rule asks. Owing no line is not being barred from one — a repair that
asked the class question anyway and found siblings may record them,
which costs a later reader nothing.
- R<n>.<k> — class: <question>; siblings: <a> (<test>, red <N> of <M>),
  <b> (<test>, red <N> of <M>)
- R<n>.<k> — class: <question>, not finitely enumerable; siblings,
  best-effort: <a> (<test>, red <N> of <M>); coverage: <what the
  enumeration reaches and what it does not>
- R<n>.<k> — repair of the instance

### Out of scope (per ticket)
Confirm nothing in this PR exceeds the ticket's scope:
- <list anything notable that was tempting but deferred>

### How to verify
Steps a reviewer or future agent can take to confirm this works:
1. `pytest tests/unit/test_modifiers.py`
2. `python -c "from core.modifiers import resolve; ..."`

### Risks / follow-ups
<known limitations, things to watch, follow-up tickets created>

### Review
Critical tier, and a change to a process document; write `N/A` otherwise.
One row per independent review round — a process-document change has one
(tier review model, "The operative test"). The total is derived from the
rows and never asserted beside them (tier review model, "When review ends").
The table appears once, here; a `BLOCKER:` comment written at the cap names
its row, and a finding's `R<n>.<k>`, rather than copying either (tier review
model, "When review ends", **One copy**).

| Round | Must-fix | Where (rules / lists / documents / tests) | Inside previous round's fix | Repaired by |
|---|---|---|---|---|
| 1 | <n> | <where> | — | <commit> |
| 2 | <n> | <where> | <m of n, k unnamed> | <commit> |

`—` where nothing was repaired; `m` and `n` count must-fixes, not findings.
`m` counts only must-fix lines whose inside-previous-fix field names a
finding from the round before, and `k` reports beside it the must-fix
lines whose field the countability sentence below leaves uncountable:
those sit neither in `m` nor out of it, and
"Repairs of repairs" in `docs/tier-review-model.md` reads this cell to
decide whether a redesign is owed, so a cell that swallowed them would let
the party the obligation sits on hold a round below "mostly". `k` is
written even when it is zero, for the reason the falsification gate writes
a zero red count as a zero: a count omitted is indistinguishable from a
count nobody took. Round 1 has no round before it, and its cell reads `—`.

Findings, per round, each in one of the two columns the tier review model
names ("What a review reports"), with the rank the reviewer gave it
(`must-fix`, `note`, or `unranked` where the reviewer gave none — three
values, because contributor policy §6 gives rank three states and repairs
an unranked finding at its class as a must-fix is; and rank does not
follow from the column: whether a finding blocks merge does not depend on
which question found it), the rule it landed on, and, where it sits inside
the repair of a finding from an earlier round, the finding whose repair it
sits inside — so that the both-columns-on-one-rule signal and the
falsifier of the class obligation in contributor policy §6 can both be
read from the record. The field is named for the case that produced it,
the previous round, and takes a finding from any earlier round. **Four
rules read it, and this is the only list of them**, so that no second list
can drift from this one: the second arm of §6's falsifier, which counts a
finding in any later round; the first arm of that falsifier and the class
signal in `docs/tier-review-model.md`, "What a review reports", which ask
about the next round alone; and the round table above, which counts the
round before. The finding's own number says which round it came from, so
one field answers all four.

The rank, the number and the rule are the reviewer's: the executor
transcribes them and does not re-rank, renumber or merge — and naming
several findings in one repair line is not a merge, since the numbers are
all there. **An absence is transcribed as an absence.** Where the reviewer
gave no rank the line reads `unranked`; where the reviewer recorded that a
finding sits inside an earlier fix without naming which, the line reads
`yes, unnamed`; where the reviewer wrote something that is neither of
those nor a finding number — a hedge such as `partly` — the line carries
the reviewer's own words. The executor writes neither a rank nor a finding
number the reviewer did not give, because a value the executor supplies is
a value the party the obligation sits on has set. **A line is countable where it
names a finding, reads `no`, or names the round the earlier fix sits in —
`yes, round 3`.** A line naming the round answers the three rules above
that need only the round; it is not counted by the second arm alone, which
needs the earlier finding's rank and so its identity. Any other value —
`yes, unnamed`, or a hedge such as `partly` — is counted by none of the
four. Such a line is reported — on the finding line, and in the count `k`
beside the round table's `m of n` — and left as the reviewer wrote it,
which is the cost of the reviewer's silence rather than something the
description may resolve. This sentence is the one statement of which lines
are countable; `k` and the rules that read the field name it rather than
restating the list. A tightening remedy carries its cost in the same
line.
- R1.1 · permits · <rank> · <rule> · <what the change permits that the
  ticket refuses> — remedy: <x>; cost, if the remedy tightens a control:
  <which ordinary changes now pay it, measured where it can be>; inside
  previous fix: <the R<n>.<k> whose repair it sits inside, `no`, `yes,
  unnamed`, or the reviewer's own words>
- R1.2 · refuses · <rank> · <rule> · <what the change refuses that honest
  work needs> — remedy: <x>; inside previous fix: <the R<n>.<k> whose
  repair it sits inside, `no`, `yes, unnamed`, or the reviewer's own
  words>
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
9. **PR description** is complete per the template above; every measured
   number in it names its baseline in the same sentence, and was read from
   a command the description names, run after the last commit that changes
   it (contributor policy §6). A number something other than its own sentence
   determines names its one site and appears in no second place, or says why
   it was kept (quality gates).
10. **No forbidden actions** taken (see `docs/ai-contributor-policy.md`, §5).
11. **Falsification gate** discharged and recorded: a red count per
    behavioural claim, a zero written as a zero.

