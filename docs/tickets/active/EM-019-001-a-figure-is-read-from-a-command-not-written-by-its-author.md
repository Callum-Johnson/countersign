---
id: EM-019-001
title: A reported figure is read from a command, not written by its author
status: in-progress
tier: critical
complexity: S
dependencies: [EM-019]
claimed_by: claude-fable-5-1
claimed_at: 2026-09-06
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

**Costs.** One command run per class of figure, not per figure. EM-016's
description carries 121 digit groups, counted by `grep -oE '\b[0-9][0-9,]*\b'`
over its `## PR Description` section at e8c4417, and they come from three
commands: `wc -w`, `git diff -w`, and one `grep -c`. Thirteen of the
descriptions in `done/` carry a figure of four digits or more, counted by
`grep -l` at the same commit. So the cost is a handful of command runs per
ticket, and the writing of the command beside the number.

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

> Leave this section empty when authoring the ticket.
