---
id: EM-022-001
title: Update ticket examples for rationale and impact metadata
status: blocked
tier: trivial
kind: maintenance
impact: enhancement
delivery: maintenance
why: "Without updated examples, adopters can copy ticket forms that omit newly required rationale and impact metadata."
complexity: S
dependencies: []
claimed_by: claude-opus-5
claimed_at: 2026-09-15
blocked_at: 2026-09-15
closed_at:
---

# EM-022-001 — Update ticket examples for rationale and impact metadata

## Why this ticket should be worked

The published ticket template sends contributors to worked examples that
predate the proposed `kind`, `impact`, `delivery`, `why` and causal
justification requirements. Leaving those examples unchanged would give an
adopter two incompatible forms to copy.

Evidence: the examples under `examples/tickets/` contain the existing
frontmatter shape and no `## Why this ticket should be worked` section.
Deferral is acceptable until EM-022 merges because the template continues to
be the current authoritative form.

**BLOCKER DISCHARGED (2026-09-15).** EM-022 merged to `main` at f465b5d, so
"Ticket rationale, impact and delivery" is present on the default branch and
the examples can demonstrate the form truthfully. The blocker text is kept as
the record of why the ticket stopped.

> BLOCKER: EM-022 must merge before examples can truthfully demonstrate its
> required ticket form. Unblock when that rule is present on the default
> branch.

Nothing else about the ticket changed; it is unclaimed and available.

**BLOCKER (2026-09-15):** the executor cannot proceed. The Specification asks
for a change that `DISCLOSURE.md` forbids, and the choice between the ways out
is a publication decision the ticket does not make.

`DISCLOSURE.md` says of `examples/`: "**These are genuine artifacts, not
written for this repository.** They are otherwise unmodified except for one
normalisation: project names and ticket identifiers were replaced with neutral
equivalents ... No other text was changed at publication, and nothing was
redacted within a published file." `examples/README.md` says the same in
shorter form.

This ticket's Files is `examples/tickets/*.md` and its Behaviour is "Every
ticket example follows the post-EM-022 template shape" — four frontmatter
fields and a `## Why this ticket should be worked` section, added to seven
genuine artifacts closed on another project between 2026-06-30 and 2026-08-21.
Doing that writes text for this repository into documents whose whole evidential
value is that none of their text was. Behaviour's second bullet — "Historical
facts remain described as historical rather than being invented" — is
satisfiable for the four fields, which are derivable from each ticket's own
Context, and cannot be satisfied for a justification section: the section asks
for the causal case its author would have made, and no such case was written.

The options the executor can see, with what each costs:

1. **Add the fields and amend the disclosure.** The seven gain the metadata
   and the section, and `DISCLOSURE.md` and `examples/README.md` are amended
   to record a retrofit across seven files. Cost: the examples stop being
   artifacts a reader can take as the original project's, and the disclosure's
   strongest sentence weakens from "unmodified except a normalisation" to
   "unmodified except a normalisation and a retrofit". That is
   addition-rather-than-exclusion, which is the inverse of the principle the
   same document states two paragraphs later: "Where an artifact needed
   redaction to be publishable, it was **excluded rather than redacted**."
2. **Demonstrate the form in the template instead.** `templates/TICKET.md`
   carries the filled-example material this ticket's own References names, and
   the new form is shown there; `examples/tickets/` is untouched, and one line
   in `examples/README.md` says the published tickets predate EM-022 and are
   published as they stood. Cost: an adopter comparing the template with the
   examples sees seven that do not follow it, mitigated but not removed by
   that line. This is the executor's recommendation, and it is not the
   executor's to choose.
3. **Annotate each of the seven.** A dated annotation per file gives the
   fields derived from its Context, in the form `adr-0038` now carries twice.
   Cost: four of the five additions belong in frontmatter, which an annotation
   at the end cannot supply, so the examples still would not "follow the
   post-EM-022 template shape"; and seven annotations for a retrofit is a
   heavier mark on the evidence than the single retrofit of option 1.

To proceed the executor needs the maintainer's choice among those, or a
fourth. Option 2 leaves `examples/` untouched and closes this ticket against a
narrowed Behaviour; options 1 and 3 change what this repository's published
evidence is, which `DISCLOSURE.md` reserves to whoever published it.

Not a reason to block, but relevant to the choice: EM-022's own rule in
`docs/ticket-lifecycle.md` binds "Every ticket written **after** this rule
takes effect". The seven examples were written in 2026, on another project,
long before it. Under the rule as written they are not out of compliance;
they are out of scope of it.

## Context

EM-022 proposes the new portable ticket fields and cites
`examples/tickets/PRJ-001-repo-skeleton.md` as a fully worked example in the
ticket template. This is a documentation follow-up discovered while applying
that change.

## Specification

### Files

- `examples/tickets/*.md` — add accurate `kind`, `impact`, `delivery` and
  `why` fields, plus the causal justification section, without changing each
  example ticket's recorded implementation evidence.

### Behaviour

- Every ticket example follows the post-EM-022 template shape.
- Historical facts remain described as historical rather than being invented
  to satisfy a new field.

## Acceptance criteria

1. Every published ticket example has all metadata and the causal
   justification section required by EM-022.
2. The examples do not change their recorded completion, review or test
   evidence.

## Out of scope

- Changing the ticket template or lifecycle rule. EM-022.
- Reclassifying real tickets outside `examples/tickets/`.

## References

- EM-022
- `templates/TICKET.md`, "Example: filled ticket"

## Notes

N/A.

## PR Description

> Leave this section empty when authoring the ticket.
