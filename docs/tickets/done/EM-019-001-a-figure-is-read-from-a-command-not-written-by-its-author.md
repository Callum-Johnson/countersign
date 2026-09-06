---
id: EM-019-001
title: A reported figure is read from a command, not written by its author
status: done
tier: critical
complexity: S
dependencies: [EM-019]
claimed_by: claude-fable-5-1
claimed_at: 2026-09-06
closed_at: 2026-09-06
---

# EM-019-001 — A reported figure is read from a command, not written by its author

## Context

Raised from EM-019, whose Out of scope named this rule and deferred it:
"Any rule about when a figure is measured. If one is wanted — that a
description's figures are taken after the last commit that changes them —
that is a rule with a cost and its own ticket."

The maintainer's observation sharpens what that rule has to say. The defect
in EM-016's three figures was not only *when* they were taken but *who*
took them. A language model is unreliable at counting and reliable at
producing a plausible count, so any rule that asks an executor to state a
number without requiring it to be read from a command's output will collect
confident wrong numbers. The executor of EM-016 knew the command, named it
in the description, ran it before the closing commit, and then wrote three
figures from an estimate of what that commit would change.

The contributor policy's §6 does not close this. It requires the baseline
in the same sentence — the commit, the branch, the date, the population —
and says nothing about where the number itself came from. EM-016's
description met §6 in full and was wrong three times, which is the evidence
that the rule as written is not the rule that was wanted.

This is the falsification gate's own demand one level up. The gate says a
claim nobody tried to break is unpinned. A figure nobody re-ran is unpinned
in the same way, and naming its baseline makes it look pinned.

## Specification

Documentation changes only.

### Files

- `docs/ai-contributor-policy.md` §6 — a bullet after the baseline bullet.
- `templates/PR-DESCRIPTION.md` — the acceptance-criteria line and the
  definition-of-done item that already point at §6.

### Public surface

N/A — this repository publishes documents. The change adds an obligation to
an existing rule and removes nothing.

### Behaviour

- A number a command can produce is **read from that command's output**,
  and the description names the command. The author does not count, and
  does not estimate what a pending edit will change.
- The command is run **after the last commit that changes what it counts**.
  Where the closing commit changes it — a note taken at close, a re-flow —
  the figure is taken again in that commit.
- Where no command can produce the number — a figure from a private
  project, a count read from another ticket's prose — the description says
  how it was obtained, which is what makes an inherited figure visible as
  one.
- The reason is stated in the document's own terms: an agent asked for a
  count produces a plausible one, and a plausible count beside a correctly
  named baseline is the most expensive kind of wrong number, because it
  survives every check the description carries.
- **Falsifier**, per "Retiring a control": retired when, over a stated
  population of closed tickets, figures reported under this rule are found
  wrong as often as the figures reported before it. The rule then costs a
  command per class of figure and catches nothing.

## What this refuses, and what it costs

**Refuses.** A figure the author knows to be true and cannot produce a
command for. It is not refused outright — the third bullet admits it — but
it must now be labelled as obtained rather than measured, on every such
figure, including ones nobody doubts.

**Costs.** One command run per class of measurement, not per number.
EM-016's description holds 121 digit groups, from

```sh
git show e8c4417:docs/tickets/done/EM-016-bound-the-brief-a-contributor-must-read.md \
  | awk '/^## PR Description/{p=1} p' | grep -oE '\b[0-9][0-9,]*\b' | wc -l
```

but most of those are ticket-id fragments, section numbers, finding numbers
and list ordinals, which are not measurements and which this rule does not
reach. Its measurements come from three commands — `wc -w`, `git diff -w`
and one `grep -c` — counted by the same pipeline with
`grep -oE '`(wc -w|git diff[^`]*|grep -c[^`]*)`' | sort -u | wc -l`. So the
cost on the wave's largest description is three runs and three command
strings written down.

Nineteen of the 21 files in `done/` — the denominator from
`git ls-tree --name-only e8c4417 docs/tickets/done/ | wc -l` — hold a
figure of four digits or more in their `## PR Description` section, from

```sh
for f in $(git ls-tree --name-only e8c4417 docs/tickets/done/); do
  git show e8c4417:$f | awk '/^## PR Description/{p=1} p' \
    | grep -qE '[0-9]{4}' && echo $f
done | wc -l
```

so the rule reaches nearly every description this repository has written.

The cost this rule does not remove: it cannot catch a figure whose command
was run against the wrong tree, only one that was never run.

## Acceptance criteria

1. AC1: `docs/ai-contributor-policy.md` §6 states that a number a command
   can produce is read from that command's output, and that the description
   names the command.
2. AC2: §6 states when the command is run, and what happens when the
   closing commit changes what it counts.
3. AC3: §6 states what a description does with a number no command can
   produce.
4. AC4: The bullet carries a **Retired when:** line.
5. AC5: `templates/PR-DESCRIPTION.md` reflects the obligation where it
   already points at §6, without restating the rule.
6. AC6: This ticket's own description states every figure with the command
   that produced it, run after the last commit that changes it. The rule is
   applied to the ticket that lands it.
7. AC7: Critical tier per ADR-0002: an independent agent that did not
   perform the work reviews this against the artifacts and records findings
   in EM-010's two columns.

## Out of scope

- Any change to §6's baseline rule itself. This adds where a number comes
  from; the baseline requirement is unchanged.
- Reporting fewer figures. That is the other answer to the same problem —
  a description that states no count cannot state a wrong one — and it
  trades evidence for safety. It is not taken here, and a maintainer who
  prefers it should say so, because the two rules pull in opposite
  directions.
- Correcting figures in already-closed descriptions. EM-019 corrected the
  three that were found; a sweep of the rest is its own ticket if wanted.
- Any mechanism that checks figures automatically. This repository has no
  gate to run one in.

## References

- EM-019 — the correction that raised this, and its deferred rule.
- EM-016 — the description that met §6 and was wrong three times.
- `docs/ai-contributor-policy.md` §6 — the rule this extends.
- `docs/quality-gates.md`, "The falsification gate" — the argument this
  borrows.

## Notes

The rule is written for the executor this repository is about. A human
contributor who miscounts is careless; an agent that miscounts is working
normally, and the document says so rather than pretending the two failures
are the same.

## PR Description

### Ticket
EM-019-001 — A reported figure is read from a command, not written by its
author

### Tier
`critical` — process-surface change (clause 5): it adds an obligation to
every pull-request description.

**Independent review obtained**, per ADR-0002: a separate agent, given the
ticket, the diff and the two questions, and not the executor's reasoning,
reviewed the change in three rounds, read-only. Findings are under Review.

### Summary
Policy §6 gains a bullet after the baseline rule. A measured number a
command can produce is read from that command's output, and the description
names the command, once for a class of figures one run produces. A measured
number is one the description asserts as a fact about a tree or its history,
such that re-running the command would confirm or refute it; a number that
names something rather than measures it is outside. The command is run after
the last commit that changes what it counts. Where no command can produce
the measurement, the description says how it was obtained.

### Acceptance criteria
- [x] AC1: §6 states that a measured number a command can produce is read
  from that command's output and that the description names the command —
  `docs/ai-contributor-policy.md`, the bullet beginning "**A measured number
  a command can produce**".
- [x] AC2: §6 states when the command is run and what the closing commit
  changes — "run the command after the last commit that changes what it
  counts, and where the closing commit changes it — a note taken at close, a
  re-flow — run it again there."
- [x] AC3: §6 states what to do with a number no command can produce —
  "Where no command can produce the measurement, say how it was obtained,
  which is what makes an inherited figure visible as one."
- [x] AC4: the bullet carries a **Retired when:** line.
- [x] AC5: `templates/PR-DESCRIPTION.md` reflects the obligation at the two
  places that already point at §6, without restating the rule.
- [x] AC6: this description states every measured figure with the command
  that produced it — below.
- [x] AC7: independent review — see Review.

### AC6 — the figures, each with its command
Every command below was run at `fe1bbf4`, which is the last commit that
changes what any of them counts; the closing commit appends this section to
a ticket file and changes none of them.

| Figure | Command | Result |
|---|---|---|
| policy words, before | `git show e8c4417:docs/ai-contributor-policy.md \| wc -w` | 2897 |
| policy words, after | `git show fe1bbf4:docs/ai-contributor-policy.md \| wc -w` | 3189 |
| template words, before | `git show e8c4417:templates/PR-DESCRIPTION.md \| wc -w` | 837 |
| template words, after | `git show fe1bbf4:templates/PR-DESCRIPTION.md \| wc -w` | 875 |
| files changed | `git diff --stat e8c4417..fe1bbf4 \| tail -1` | 5 files, 291 insertions, 4 deletions |

The rule costs this repository 330 words across two documents, by
subtraction from the rows above. The reviewer re-ran every command in each
round and reported the same results.

`EM-019-001`, `§6`, `e8c4417`, `AC6` and the round numbers in the table
below name things rather than measure them, and are outside the rule this
ticket lands. That is the distinction the third round drew, and this
description is the first artifact written under it.

### Falsification
N/A — no behavioural claim. What a reader does differently, per criterion:
- AC1, AC2: an author who would have written a count from memory runs a
  command, quotes it, and re-runs it if the closing commit moves it.
- AC3: an inherited figure is labelled as obtained, so a later reader knows
  not to try deriving it from this tree.
- AC4: a maintainer with a population of closed tickets can retire the rule
  on evidence.
- AC5, AC6: the obligation is visible where a description is written, and
  this description is its first instance.

Repairs of this review's findings, in the class form policy §6 asks for.
There is no suite, so each sibling says what a reader would do differently.
- R2.3 — class: **which numbers in a description does this rule reach?**
  The first answer enumerated token kinds, which is an enumeration against
  an author's ingenuity, and it placed a date outside the rule while the
  bullet above names a date as a baseline. Siblings the property must
  decide, and does: a count (inside), a size (inside), a date (inside, and
  the contradiction is gone), a proportion (inside), a ticket id (outside),
  a section number (outside), a finding number (outside), a list ordinal
  (outside). The test is whether a command could disagree with the number.
  What a reader does differently: decides a case the examples do not cover
  by applying the test, instead of looking for it in a list.
- R1.1 — repair of the instance, and not a documentation defect at all:
  see the process failure recorded below.
- R1.2, R1.3, R1.4, R2.4, R2.5 — repair of the instance, each: an indent,
  two figures restated with their pipelines, a denominator, a re-flow.

### Out of scope (per ticket)
Confirmed: §6's baseline rule is unchanged apart from an indent this change
had disturbed and restored; no cap on how many figures a description
reports; no closed description swept; no automatic check.

Recorded, not changed: R1.7, this rule's falsifier names no minimum
population, so on a project with no history it compares nought with nought.
Every falsifier in these documents but one shares that shape, and naming a
floor here would be a number the project has no evidence for.

R3.1, a note left open by agreement: a section number is given as something
that names, yet a command could disagree with `§6` if sections were
renumbered. The example resolves it; the remedy, if it is ever wanted, is
"could disagree with the number *as a measurement*".

### A process failure, recorded
The first attempt at this ticket never branched and never claimed. A board
edit inside the raise script failed against a row that was already correct,
which broke the command chain, so the branch was never created and two
commits landed on `main` against a ticket still sitting in `ready/`. The
review caught the symptom as R1.1 — a claim commit that performed none of
the claiming steps — and the cause was worse than the symptom looked.

The three commits were unpushed. They were reset and the sequence redone in
order: raise on `main`, branch, claim, work. Nothing that had been pushed
was rewritten. It is recorded here rather than tidied away because the
lifecycle's crude lock is the file move, and this is what it looks like when
an executor skips it: the ticket's own record would never have said who did
the work.

### Review
| Round | Must-fix | Where (rules / lists / documents / tests) | Inside previous round's fix | Repaired by |
|---|---|---|---|---|
| 1 | 5 (of 9 findings) | documents and process: the claim performed none of the claiming steps (must-fix); an indent disturbed on a bullet the ticket put out of scope (must-fix); a cost figure unreproducible under the words describing it (must-fix); a cost claim that did not follow from its own figures (must-fix); the rule's subject silently widened from measured numbers to all numbers (must-fix); the definition-of-done item restating the rule without a reference; no decision record against the trigger list; a falsifier with no minimum population; one command named per number where one run yields many | — | a4e642c |
| 2 | 1 (of 3 findings) | documents: the exclusion list placed a date outside the rule while the bullet above names a date as a baseline (must-fix); a denominator without a command; a ragged paragraph | 1 of 1 | fe1bbf4 |
| 3 | 0 (of 1 note) | documents: a section number sits at the edge of the property's own test | 1 of 1 | recorded, not changed |

Derived total: 6 must-fix over three rounds.

**The class signal fired, and was answered as a redesign.** Round 2's
must-fix was a first-column finding on the same rule as round 1's, one round
later and inside round 1's fix. The reviewer named the signal rather than
proposing a third adjustment, and recorded beside it the adjustment it would
otherwise have proposed — strike "a date" from the exclusion list — so that
the judgement could be checked. The executor took the redesign: the line is
now a property rather than a list. Round 3 found no finding on that rule in
either column, which is what the signal's own falsifier would have counted
against it had the redesign bought nothing.

Round 1 by column and rule — permits: R1.1, the lifecycle's Claiming rule;
R1.2, the baseline bullet; R1.3 and R1.4, this rule, applied to the ticket
that lands it; R1.5, the definition-of-done item; R1.6, the decision-record
trigger, raised as EM-019-001-001; R1.7, this rule's falsifier, recorded.
Refuses: R2.1, this rule's subject, which as written reached every
identifier and ordinal in a description; R2.2, the naming clause, which read
as one command per number.

**On review isolation.** The reviewer disclosed writing one scratch file
outside the repository during round 1, before switching to pipes, and
re-derived every figure without it. The tree under review was clean at the
end of every round, by `git status --porcelain` and `git worktree list`, so
nothing is a finding against the review under "Review isolation", whose rule
is about the tree under review.

### How to verify
Re-run the five commands in the AC6 table. Then
`grep -n "measured number" docs/ai-contributor-policy.md` — the rule and the
baseline bullet it inherits from, in that order.

### Risks / follow-ups
- **EM-019-001-001** (raised here): seven rule-adding tickets produced no
  decision record, against a trigger list that appears to require one.
- The rule cannot catch a figure whose command was run against the wrong
  tree, only one that was never run. Its falsifier measures whether that
  gap matters.
- This is the fourth rule this repository has added to a description's
  obligations. The map EM-016 landed makes them findable; nothing yet
  bounds how many there are.

