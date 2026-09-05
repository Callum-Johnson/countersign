---
id: EM-014
title: A rule states its own falsifier, and a control can be retired
status: ready
tier: critical
complexity: M
dependencies: [EM-010]
---

# EM-014 — A rule states its own falsifier

## Context

EM-006 demands of every test that it name the wrong implementation it rules
out, and calls a test that cannot do so decorative. EM-007 makes the same
demand of a review: say what a converged review looks like, or you cannot
show it converged, only that it stopped. Nobody makes the demand of a rule.

The wave EM-006 to EM-012 shows why that matters. Each of the seven adds to
the brief; each says in its own words that it removes nothing — "no existing
rule is deleted", "adds to the reviewer's brief and removes nothing from it",
"adds a constraint", "adds a path and removes none". Six of the seven are
first-column tickets in EM-010's terms. The wave that diagnoses monotonic
tightening is, at the level of the documents it edits, a monotonic
tightening, and nothing in this repository could have said so, because nothing
in this repository asks a rule what would retire it.

EM-010 gives a review the means to *find* that a rule refuses honest work.
There is then nowhere for the finding to go. A superseded decision record is
kept and marked; a rule in `docs/` has no superseded state, no retired state,
and no stated condition under which either would apply. A control set that can
only grow is over-tightening by construction, whatever its review brief says,
and a reader adopting these documents inherits that property without being
told.

The demand is the same one already made twice. A rule that cannot say what
evidence would retire it is an unpinned rule, in exactly the sense that a test
with a zero red count is an unpinned test: it is there, it is passed, and it
constrains nothing that can be checked.

## Specification

Documentation changes only.

### Files

- `docs/tier-review-model.md` — a new section, "Retiring a control", after
  the section EM-010 introduces.
- Every rule-bearing document under `docs/` — `ai-contributor-policy.md`,
  `tier-review-model.md`, `quality-gates.md`, `ticket-lifecycle.md`,
  `adr-process.md` — gains, per rule or per section of rules, a one-line
  statement introduced by **Retired when:**.
- `docs/retired/` — the directory a retired rule's text moves to, with the
  evidence that retired it. Created by the first retirement, not by this
  ticket.
- `templates/TICKET.md` — the ticket template gains, in the Behaviour
  section's guidance, that a ticket adding a rule states the rule's
  falsifier.

### Public surface

N/A — this repository publishes documents. The change adds one obligation to
every rule and a path that did not exist.

### Behaviour

- Every control stated in `docs/` carries a **Retired when:** line naming
  the evidence that would show the control refuses honest work, or no longer
  catches what it was added to catch. The evidence is stated so that a
  reviewer could recognise it: a measured cost, a class of change it blocks
  that the project needs, a failure mode it was added for that a later
  control now covers.
- A rule whose falsifier cannot be stated is recorded in those words —
  "no falsifier stated" — in the same place. That is permitted, as EM-009
  permits "repair of the instance", and for the same reason: it is a claim a
  reviewer can see and hold the author to, where silence is not. A rule that
  says "no falsifier stated" is the rule most worth a second look.
- A falsifier may be a cost rather than a failure. "Do not force-push to the
  main branch" has no observed failure that retires it; its falsifier is the
  cost side — retired when the project's history model changes such that
  the rule protects nothing. Stating a cost-side falsifier is not a weaker
  form; it is the form most rules take.
- A second-column finding under EM-010 that matches a rule's stated
  falsifier **retires the rule**, and does not amend it. Retirement is a
  ticket, critical tier under the operative test's process-surface clause,
  and it moves the rule's text and the retiring evidence to `docs/retired/`
  together. Retired rules are kept for the reason superseded decision
  records are kept: the record of what was tried and why it stopped is most
  of the value.
- A second-column finding that does *not* match the stated falsifier is a
  finding against the falsifier as much as against the rule: either the
  rule is refusing something its author did not foresee, in which case the
  falsifier was too narrow and is widened in the same ticket, or the finding
  is wrong. The review says which.
- A ticket that adds a rule states the rule's falsifier in its Behaviour
  section. A ticket that adds a rule without one is not ready, in the sense
  the ticket template uses that word.

## What this refuses, and what it costs

Applying EM-010's two questions to this ticket, as the wave's other tickets
now do.

**Refuses.**

- A rule added without a stated falsifier, or without the words "no
  falsifier stated". This is a refusal of quick rules, and it is meant to be.
- Amending a rule that a second-column finding has matched. The path is
  retire-and-replace, which is heavier than an edit; a rule that needs a
  small correction and whose falsifier was matched only technically pays the
  full retirement.

**Costs.**

- One line per rule across five documents. Counting a rule as a bullet or a
  bold-led paragraph in those documents at 8b0a8b4 gives on the order of
  forty; the implementer counts and states the figure. Roughly forty short
  sentences, written once.
- The thinking cost is the real one, and it is the point. Stating a
  falsifier for a rule the author is fond of is uncomfortable in the way
  naming a test's mutant is uncomfortable, and for the same reason.
- Retirement tickets are critical tier. A project that retires often pays a
  review for each; the wave's own experience says reviews of process
  documents can run long. EM-007's cap applies.

## Acceptance criteria

1. AC1: `docs/tier-review-model.md` states, in its own section, that a
   second-column finding matching a rule's stated falsifier retires the rule
   rather than amending it, where the retired text goes, and that the
   record is kept.
2. AC2: Every rule-bearing document under `docs/` carries a **Retired when:**
   line per rule or per section of rules, or the words "no falsifier stated"
   in its place, and the implementer's count of rules is stated in the
   pull-request description with the baseline it was counted at.
3. AC3: The section states that a falsifier may be cost-side, with the
   force-push rule as the example.
4. AC4: The section states what happens when a second-column finding does not
   match the stated falsifier.
5. AC5: `templates/TICKET.md` states that a ticket adding a rule states its
   falsifier, in one sentence, referencing the section for the rule.
6. AC6: This ticket's own rule carries its falsifier, stated in Notes, and
   the falsifier is one a reviewer could recognise.
7. AC7: No existing rule is retired by this ticket. The path is created;
   walking it is a separate ticket each time.
8. AC8: Critical tier per ADR-0002: an independent agent that did not perform
   the work reviews this against the artifacts and records findings in the
   pull-request description, in EM-010's two columns.

## Out of scope

- Retiring anything now, including anything in the wave. AC7.
- Stating falsifiers for the rules the wave adds. Each wave ticket adds its
  own, in its own Behaviour section, once this ticket lands and the template
  requires it. Until then the wave's tickets carry the *refuses and costs*
  sections added 2026-09-05, which are the same question asked of the ticket
  rather than of the rule.
- Any mechanism for tracking falsifiers over time — a register, a review
  cadence. If one is wanted it is a later ticket with evidence from this one.

## References

- EM-006 — the falsification gate this ticket generalises from tests to
  rules.
- EM-007 — the stopping rule, which makes the same demand of reviews.
- EM-010 — the second column, whose findings this ticket gives somewhere to
  go.
- EM-009 — "repair of the instance", the model for "no falsifier stated".
- `docs/adr-process.md` — superseded decision records are kept; retired rules
  are kept for the same reason.
- `docs/tier-review-model.md`, the scrutiny-list section — "an escalation
  everyone ignores is worse than none", which is the cost this ticket gives a
  path out of.

## Notes

**This ticket's own falsifier.** Retired when, after twenty rules carry
stated falsifiers, second-column findings against those rules have
accumulated and none has matched a stated falsifier. That would show the
falsifiers are decorative — written to satisfy the rule, not to be
recognised — and a decorative falsifier is the defect this ticket exists to
remove, so the ticket would have failed on its own terms.

**Why retire rather than amend.** An amended rule keeps its place in the
document and its authority with readers, and the amendment is invisible to
anyone who did not read the diff. A retired rule leaves a gap a reader can
see and a record a reader can find. The wave's own tickets argue that the
record is where the value is; this applies the argument to the rules the
tickets add.

**Why the wave's tickets got a section rather than falsifiers.** The
falsifier belongs to the rule and is stated in the ticket that adds it. The
wave's tickets were authored before this obligation existed, and the honest
retrofit is EM-010's question asked of each ticket — what it refuses, what
it costs — which is what was added. When each wave ticket is worked, its
implementer states the falsifier for the rule it lands, per this ticket's
template change. That is also the first test of whether stating one is as
hard as this ticket claims.

**Working this with the wave.** This ticket reads EM-010's second column, so
it depends on EM-010. It is otherwise separable, and the maintainer may
decline it on its own. If the wave is reviewed as one change, this ticket
should be reviewed with it, because it is the wave's answer to the question
the wave did not ask.

## PR Description

> Leave this section empty when authoring the ticket.
