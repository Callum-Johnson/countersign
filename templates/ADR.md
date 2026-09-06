# ADR-NNNN: <short title>

- **Status:** proposed | accepted | superseded by ADR-MMMM | withdrawn
- **Date:** YYYY-MM-DD
- **Deciders:** <agent identifiers or roles>
- **Related:** <ticket IDs, other ADR IDs, sections of the adopting project's own DESIGN.md>

## Context

What is the problem? Why does it need a decision? What was the trigger
— a specific ticket, a bug, a constraint that emerged during
implementation? Two to five short paragraphs. Reference the sections of
the adopting project's own DESIGN.md that this ADR supplements or
contradicts.

## Decision

The decision in plain language. One paragraph if possible. Be
unambiguous: a reader six months from now should know exactly what was
agreed.

If the decision can be summarised as code or configuration, include it:

```python
# Example
TYPE_X = "new_value"
```

## Rationale

Why this decision and not the alternatives. Lead with the most
compelling reason. Address obvious objections.

## Consequences

What does this decision lock in? What becomes harder? What becomes
easier? List both positive and negative consequences honestly.

- Positive: <e.g. "now possible to ..." >
- Negative: <e.g. "requires migration of ..." >
- Neutral: <e.g. "changes the public API of ..." >

## Alternatives considered

For each: one paragraph on what it was, and why it was rejected.

### Alternative 1: <name>

Description. Why rejected.

### Alternative 2: <name>

Description. Why rejected.

## Migration

If this decision changes existing code, what is the migration plan?
Which tickets capture the work? If no migration is needed (greenfield
decision), write "N/A".

---

## How to use this template

1. Copy to `docs/adr/NNNN-<kebab-case-slug>.md` where `NNNN` is the next
   sequential 4-digit number (check existing ADRs).
2. Fill in every section. `N/A` is acceptable for Migration if not
   applicable; other sections must be substantive.
3. Status starts as `proposed`. Move to `accepted` when the PR
   introducing the change merges.
4. If a later ADR overrides this one, set status to
   `superseded by ADR-MMMM` and add a link at the top to the new ADR.
   Do not delete superseded ADRs — they are the project's decision
   history.

## When to write an ADR vs not

Write one when:

- A library is added or swapped.
- A public engine API shape changes.
- A locked decision in the adopting project's own DESIGN.md needs revision.
- A new top-level package is added.
- A workflow rule in `docs/ai-contributor-policy.md`, `docs/ticket-lifecycle.md`
  or `docs/tier-review-model.md` changes.

Do **not** write one for:

- Routine implementation choices internal to a single module.
- Renaming a function (just rename it).
- Test-only changes.
- Configuration tweaks that any developer would make.

When in doubt: if the decision affects multiple tickets or constrains
future work, ADR it. If it only affects this one ticket, the ticket
itself is enough.
