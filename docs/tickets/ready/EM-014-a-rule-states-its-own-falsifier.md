---
id: EM-014
title: A rule states its own falsifier, and a control can be retired
status: ready
tier: critical
complexity: M
dependencies: [EM-007, EM-010]
---

# EM-014 — A rule states its own falsifier, and a control can be retired

## Context

EM-006 demands of every test that it name the wrong implementation it rules
out, and calls a test that cannot do so decorative. EM-007 makes the same
demand of a review: say what a converged review looks like, or you cannot
show it converged, only that it stopped. Nobody makes the demand of a rule.

The wave EM-006 to EM-012 shows why that matters. Each of the seven adds to
the brief. Six say so in their own words: EM-007 "adds to that set without
changing an existing rule"; EM-008 "adds a trigger to an existing rule and
changes no rule's procedure"; EM-009 "adds an obligation to an existing
gate"; EM-010 "adds to the reviewer's brief and removes nothing from it";
EM-011 "adds a constraint on how review is conducted and changes nothing
about what it examines"; EM-012 "adds a path through the lifecycle and
removes none". EM-006 annotates one published pattern in place, adds several
rules, and says "no existing rule is deleted without a stated replacement".
Five of the seven are
first-column tickets in EM-010's terms; EM-007 is mixed; EM-012 is the one
loosening. The wave that diagnoses monotonic tightening is, at the level of
the documents it edits, a monotonic tightening, and nothing in this
repository could have said so, because nothing in this repository asks a
rule what would retire it.

EM-010 gives a review the means to *find* that a rule refuses honest work.
There is then nowhere for the finding to go. A superseded decision record is
kept and marked; a rule in `docs/` has no superseded state and no stated
condition under which one would apply. A control set that can only grow is
over-tightening by construction, whatever its review brief says, and a
reader adopting these documents inherits that property without being told.

The demand is the one already made twice. A rule that cannot say what
evidence would retire it is an unpinned rule, in exactly the sense that a
test with a zero red count is an unpinned test: it is there, it is passed,
and it constrains nothing that can be checked.

## Specification

Documentation changes only.

### Files

- `docs/tier-review-model.md` — a new section, "Retiring a control", after
  the section EM-010 introduces.
- Every rule-bearing document under `docs/` — `ai-contributor-policy.md`,
  `tier-review-model.md`, `quality-gates.md`, `ticket-lifecycle.md`,
  `adr-process.md` — gains, per rule or per section of rules, a one-line
  statement introduced by **Retired when:**.
- `docs/adr-process.md` — "When to write one" already lists "a workflow rule
  changes"; it gains one sentence stating that a retirement or amendment
  under this ticket is that case, and that the ADR carries the rule's text
  as it stood, the finding that matched, and the text that replaces it if
  any.
- `templates/TICKET.md` — the guidance on the Behaviour section gains one
  sentence: a ticket adding a rule states the rule's falsifier.

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
- A rule stated in two documents — hooks may not be skipped appears in the
  contributor policy and in the quality gates — carries one falsifier,
  stated in the contributor policy and referenced from the quality gates.
- A second-column finding under EM-010 that matches the stated falsifier of
  a rule **already in `docs/` at the change's baseline** is handled by
  extending EM-007's second condition from the round to the finding: the
  finding lies inside a limit the rule itself recorded, so it goes to a
  ticket that owns it, raised if it does not exist, and that one must-fix is
  discharged by raising it. That ticket is a **retirement ticket**, critical
  tier under the operative test's process-surface clause. It produces a
  decision record per `docs/adr-process.md`, which carries the rule's text as
  it stood and the finding that matched, and the rule leaves the document.
  Retired rules are kept in the record for the reason superseded decision
  records are kept: what was tried and why it stopped is most of the value.
- A second-column finding that matches the falsifier of a rule **the change
  under review itself adds** is a must-fix on the change, repaired in the
  round like any other. The defective rule does not ship and then get
  retired; it does not ship.
- **Amendment with record.** Where the match is technical and the correction
  small — a word, a scope, a threshold — the retirement ticket may amend the
  rule in place instead of removing it, provided the decision record carries
  the old text, the matching finding, and the new text. The record is the
  control; the removal is not. A ticket choosing amendment says in its
  pull-request description why the match was technical.
- A second-column finding that does *not* match the stated falsifier is a
  finding against the falsifier as much as against the rule: either the
  rule is refusing something its author did not foresee, in which case the
  falsifier was too narrow and is widened in the same ticket, or the finding
  is wrong. The review says which.
- A ticket raised after this ticket closes that adds a rule states the
  rule's falsifier in its Behaviour section, and a ticket that does not is
  not ready, in the sense the ticket template uses that word. Rule-adding
  tickets already in `ready/` when this ticket closes are not affected; each
  states the falsifier for the rule it adds when it is worked, and its
  pull-request description says so. A rule-adding ticket raised between this
  ticket's raise and its close states its falsifier if it can and says "no
  falsifier stated" if not. The exempt tickets are named in the decision
  record that lands this ticket, not in the model, which adopting projects
  read.
- **This ticket's own falsifier.** Retired when twenty rules carry stated
  falsifiers, ten second-column findings have been recorded against rules
  that carry one, and none has matched. That would show the falsifiers are
  decorative — written to satisfy this rule, not to be recognised — and a
  decorative falsifier is the defect this ticket exists to remove.

## What this refuses, and what it costs

Applying EM-010's two questions to this ticket, as the wave's other tickets
now do.

**Refuses.**

- A rule added after this closes without a stated falsifier or the words
  "no falsifier stated". This is a refusal of quick rules, and it is meant to
  be.
- Removal without a record, and amendment without a record. Both paths
  exist; neither is free.

**Costs.**

- One line per rule across five documents. Counting a rule as a list item or
  a bold-led paragraph outside code fences and tables, at 8b0a8b4, gives 52
  — ai-contributor-policy 27, tier-review-model 9, quality-gates 0,
  ticket-lifecycle 7, adr-process 9 — and that method cannot see
  quality-gates' five rules, which are headings, while it does see seven
  checklist items and seven procedure steps that are arguably not rules. A
  defensible count is between 43 and 57 — the five heading rules in, the
  fourteen steps in or out — depending on what a rule is.
  The implementer states the method used and the count it gives.
- The thinking cost is the real one, and it is the point. Stating a
  falsifier for a rule the author is fond of is uncomfortable in the way
  naming a test's mutant is uncomfortable, and for the same reason.
- Retirement and amendment tickets are critical tier. A project that retires
  often pays a review for each; the wave's own experience says reviews of
  process documents can run long. EM-007's cap applies.

## Acceptance criteria

1. AC1: `docs/tier-review-model.md` states, in its own section, that a
   second-column finding matching the stated falsifier of a rule at the
   baseline goes to a retirement ticket by extending EM-007's second
   condition to the finding, that the must-fix is discharged by raising it,
   that a rule the change itself adds is repaired in the round instead, and
   that the outcome is a decision record carrying the rule's text and the
   finding.
2. AC2: Every rule-bearing document under `docs/` carries a **Retired when:**
   line per rule or per section of rules, or the words "no falsifier stated"
   in its place, and the pull-request description states the counting method
   used and the count it gave, against the 52-by-list-items figure at
   8b0a8b4 above.
3. AC3: The section states that a falsifier may be cost-side, with the
   force-push rule as the example.
4. AC4: The section states what happens when a second-column finding does not
   match the stated falsifier.
5. AC5: The section states the amendment-with-record path and what the
   record must carry.
6. AC6: `docs/adr-process.md` states that retirement and amendment produce a
   decision record and what it carries, in one or two sentences, without
   restating the section.
7. AC7: `templates/TICKET.md` states that a ticket adding a rule states its
   falsifier, in one sentence, referencing the section for the rule.
8. AC8: The section states that the falsifier obligation applies to tickets
   raised after this ticket closes and that rule-adding tickets already in
   `ready/` are exempt; the exempt tickets are named in the decision record
   that lands this ticket, and the section does not list ticket ids.
9. AC9: This ticket's own falsifier is stated in its Behaviour section, with
   the two counts a reviewer would check.
10. AC10: No existing rule is retired or amended by this ticket. The path is
    created; walking it is a separate ticket each time.
11. AC11: A rule stated in two documents carries one falsifier, and the
    hooks rule is the worked example.
12. AC12: Critical tier per ADR-0002: an independent agent that did not
    perform the work reviews this against the artifacts and records findings
    in the pull-request description, in EM-010's two columns.

## Out of scope

- Retiring or amending anything now, including anything in the wave. AC10.
- Stating falsifiers for the rules the wave adds, or for EM-014-001's. Each
  such ticket states its
  own when it is worked; until then the wave's tickets carry the *refuses and
  costs* sections added 2026-09-05, which are the same question asked of the
  ticket rather than of the rule.
- A `docs/retired/` directory or any record parallel to the decision
  records. The first draft of this ticket proposed one; independent review
  found that `docs/adr-process.md` already requires a decision record when a
  workflow rule changes, and one record for one event is the right number.
- Adding a *refuses and costs* section to the ticket template. Nine tickets
  carry one as a retrofit. Whether every ticket should is a separate decision
  with the cost of one more mandatory section, and is not decided here.
- Any mechanism for tracking falsifiers over time — a register, a review
  cadence. If one is wanted it is a later ticket with evidence from this one.

## References

- EM-006 — the falsification gate this ticket generalises from tests to
  rules.
- EM-007 — the stopping rule, whose second condition routes a matched
  finding; a hard dependency, since this ticket's text reads that condition.
- EM-010 — the second column, whose findings this ticket gives somewhere to
  go; a hard dependency, since the new section follows the section EM-010
  introduces.
- EM-009 — "repair of the instance", the model for "no falsifier stated".
  Cited as a model, not depended on.
- `docs/adr-process.md` — superseded decision records are kept; retired
  rules are kept in the same record for the same reason.
- `docs/tier-review-model.md`, the scrutiny-list section — "an escalation
  everyone ignores is worse than none", which is the cost this ticket gives a
  path out of.

## Notes

**Why retire rather than amend by default.** An amended rule keeps its place
in the document and its authority with readers, and the amendment is
invisible to anyone who did not read the diff. A retired rule leaves a gap a
reader can see and a record a reader can find. Amendment with record is the
proportionate path for a technical match, and the record requirement is what
keeps it from being the invisible edit.

**On landing order.** This ticket depends on EM-007 and EM-010 because its
section text references EM-007's second condition and follows EM-010's
section. If either lands in a different form than its ticket specifies — EM-
010's Files allows its section to be an extension rather than a new section —
the implementer places this ticket's section where EM-010's text landed and
says so.

**Why the wave's tickets got a section rather than falsifiers.** The
falsifier belongs to the rule and is stated in the ticket that adds it. The
wave's tickets were authored before this obligation existed, and the honest
retrofit is EM-010's question asked of each ticket — what it refuses, what
it costs — which is what was added. When each wave ticket is worked, its
implementer states the falsifier for the rule it lands. That is also the
first test of whether stating one is as hard as this ticket claims.

**Working this with the wave.** If the wave is reviewed as one change, this
ticket should be reviewed with it, because it is the wave's answer to the
question the wave did not ask.

## PR Description

> Leave this section empty when authoring the ticket.
