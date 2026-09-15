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

`docs/adr-process.md`, "When to write one", states this in full: the triggers,
the cases that are not triggers, the test that settles the rest, and what the
trigger reaches. It is not restated here, per `docs/tier-review-model.md`,
"Retiring a control" — a rule stated in two documents carries one falsifier, at
the place it is stated in full, and referencing it from the other is what keeps
the two from drifting.

Two things that document settles and a shorter list here got wrong, named so a
reader knows what the reference is carrying: a rule **retired or amended** under
"Retiring a control" is a trigger, because there the record is the control and
the retired text survives nowhere else; and a rule merely **added inside a
document under a decision already taken** is not one, whatever it constrains,
because the constraint is that decision's and that decision has its record.

An adopting project copying this template takes `docs/adr-process.md` with it,
as the README's "Start here" table directs; the template names it rather than
carrying a copy that can fall behind.
