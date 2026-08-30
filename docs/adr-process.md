# Architecture decision records

A decision record captures a choice that constrains future work, together with
the reasoning and the alternatives that were rejected.

## When to write one

Write an ADR when:

- A dependency is added or swapped.
- A public API shape changes.
- A previously locked design decision is revised.
- A new top-level package appears.
- A workflow rule changes.

Do **not** write one for:

- Implementation choices internal to one module.
- Renaming something.
- Test-only changes.
- Configuration any contributor would make.

The test: if the decision affects multiple tickets or constrains future work,
it is an ADR. If it affects only the ticket in hand, the ticket is enough.

## Structure

Context, Decision, Rationale, Consequences (positive, negative and neutral,
stated honestly), Alternatives considered, Migration. Every section is filled;
`N/A` is written explicitly where a section genuinely does not apply.

Status begins `proposed` and becomes `accepted` when the change merges. A
superseded ADR is marked `superseded by ADR-NNNN` and **kept** — the record is
the decision history, and deleting the wrong turns destroys most of its value.

See [the template](../templates/ADR.md).

## Why this matters more with AI contributors

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
