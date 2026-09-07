# Architecture decision records

A decision record captures a choice that constrains future work, together with
the reasoning and the alternatives that were rejected.

## When to write one

Write an ADR when:

- A dependency is added or swapped.
- A public API shape changes.
- A previously locked design decision is revised.
- A new top-level package appears.
- A workflow rule changes — including a rule retired or amended under
  `docs/tier-review-model.md`, "Retiring a control". That record carries the
  rule's text as it stood, the finding that matched its falsifier, and the
  text that replaces it, if any.

Do **not** write one for:

- Implementation choices internal to one module.
- Renaming something.
- Test-only changes.
- Configuration any contributor would make.

The test: if the decision affects multiple tickets or constrains future work,
it is an ADR. If it affects only the ticket in hand, the ticket is enough.

**Retired when:** a regression a recorded decision would have prevented
happens with the record present, more than once over a stated population, or
the set of records grows past what a contributor reads before a first edit;
the trigger list is then producing records nobody reads.

**What "a workflow rule changes" reaches.** The trigger reaches a decision
that changes how the process itself is governed — the form every rule takes,
who may review or approve, whether the process applies to the repository at
all — and a rule retired or amended under "Retiring a control", which the
trigger names because there the record is the control: the retired text
leaves the document, and the record is the only place it and the finding
that matched survive. It does not reach a rule added inside a document, or
extended in place one rule at a time, under an existing decision — one that
changes what the process asks at one step, when to block, what a repair
carries, where a review runs, and sits under the decision that put that
step there. Such a rule stays in the document with its falsifier, and its
ticket is its record: the Context names what it was written from, the
ticket file states the rule and its falsifier — or, for a rule that predates
ADR-0003, EM-014's migration wrote the falsifier, which the document carries
— and the pull-request description records the review, so a decision record
would carry the same content a second time. Those clauses decide a case;
the three that follow show them applied.
ADR-0003 is on the first side: the falsifier obligation changed how every
rule in `docs/` is written and how the set can shrink, and no document could
have carried it as one rule among the others. EM-011's review-isolation rule,
`docs/quality-gates.md`, "Review isolation", is on the second: it says where
the review ADR-0002 decided on runs, and was added under that decision.
EM-021's second-instance bar sits nearest the line and on the second side:
it says what a rule-adding ticket carries before its rule enters, and was
added as one paragraph under ADR-0003's decision that a rule is held to
evidence — ADR-0003's migration added a line to every rule in `docs/`, and
EM-021 rewrote none. The section's test above reads the same way: the
constraint such a rule places on future work is the existing decision's,
applied at one step, and that decision has its record. This is the practice
this repository has followed — the rules added by EM-008, EM-009, EM-010,
EM-011, EM-012, EM-016 and EM-019-001 produced no record, and under this
line none was owed. The line decides whether a record is owed and nothing
about tier: a rule added to a process document is a process-surface change
under the operative test either way.

**Retired when:** a rule added under an existing decision, and therefore
recorded in no decision record, is found to have been undone or contradicted
by a later contributor who could not see why it was there, more than once
over a stated population of merged changes. The line is then drawn too
narrowly, and the trigger reaches those rules after all.

## Structure

Context, Decision, Rationale, Consequences (positive, negative and neutral,
stated honestly), Alternatives considered, Migration. Every section is filled;
`N/A` is written explicitly where a section genuinely does not apply.

Status begins `proposed` and becomes `accepted` when the change merges. A
superseded ADR is marked `superseded by ADR-NNNN` and **kept** — the record is
the decision history, and deleting the wrong turns destroys most of its value.

See [the template](../templates/ADR.md).

**Retired when:** a section is `N/A` in most records over a stated population
— the structure then asks questions the decisions do not have — or decision
history is kept somewhere the superseded record is not needed.

## Why this matters more with AI contributors

*Not a rule.* This section explains the rules above and constrains nothing; it
carries no falsifier.

The no-shared-memory rule means an agent cannot ask why something is the way it
is. It can only read.

Without decision records, an agent encountering an unusual choice has two
options: work around it, or "fix" it. Both are bad, and the second is worse
because it is confident. A recorded decision with its rationale is the only
mechanism that reliably prevents a later contributor from undoing a deliberate
choice it mistook for an accident.

This is the single highest-leverage document type in the system. Thirty-nine
of them accumulated in two months on one project, and the ones that earned
their keep were almost never the ones that felt important when written — they
were the ones that stopped a plausible-looking regression a month later.

## Decisions about the process are themselves ADRs

The ticket lineage scheme, the tier trigger, and the review model each have a
decision record. Changing the process is a process-surface change, which the
operative test classifies as `critical`, which means it needs a second
reviewer.

A governance system that cannot be changed becomes a system people route
around. One that can be changed silently is not a control. Recording process
changes the same way as technical ones is what keeps it honest.

**Retired when:** the tier model ceases to class the process surface as
`critical`, at which point this rule's second sentence is false and its first
stands alone.
