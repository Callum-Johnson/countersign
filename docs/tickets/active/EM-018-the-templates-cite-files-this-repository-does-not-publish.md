---
id: EM-018
title: The templates cite files this repository does not publish
status: in-progress
tier: standard
complexity: S
dependencies: []
claimed_by: claude-fable-5-1
claimed_at: 2026-09-06
---

# EM-018 — The templates cite files this repository does not publish

## Context

Found on 2026-09-06 during an assessment of the repository at 0947dda, by
grepping the published templates for references to files that do not exist
here. The templates are the part of this repository most likely to be
copied — the licence says they "are intended to be copied and adapted", and
DISCLOSURE records that they were "derived from the working versions" of a
private project. They still carry that project's furniture:

- `templates/TICKET.md`: `phase: 1 # 1-8, matches DESIGN.md §8` in the
  frontmatter; "Link to the DESIGN.md section(s) it advances"; "belongs in
  `backlog/` rather than `ready/`"; "See CONTRIBUTING.md §3 for the
  required sub-section structure"; "See AGENTS.md ... and CONTRIBUTING.md
  §6–§7 for the full procedures"; "Set `tier` per the rubric in
  CONTRIBUTING.md §4"; a worked example at a path that does not exist here.
- `templates/PR-DESCRIPTION.md`: "No forbidden actions taken (see
  AGENTS.md)".
- `templates/ADR.md`: "Reference DESIGN.md sections"; "A locked decision in
  DESIGN.md needs revision"; "A workflow rule in CONTRIBUTING.md changes".

`DESIGN.md`, `CONTRIBUTING.md`, `AGENTS.md` and `backlog/` are not in this
repository and are not described anywhere in it. An adopter copying a
template is sent to four files they do not have, for four answers this
repository does publish under other names. No EM ticket uses the `phase`
field.

## Specification

Documentation changes only. The templates keep their structure; their
references resolve.

### Files

- `templates/TICKET.md`
- `templates/PR-DESCRIPTION.md`
- `templates/ADR.md`

### Public surface

The templates are the surface an adopter copies. Their references are
instructions an adopter follows, which is why this is not a cosmetic fix.

### Behaviour

- Every reference to a file resolves within this repository, or says
  plainly that it names a document the adopting project keeps and this one
  does not publish.
- `AGENTS.md` becomes `docs/ai-contributor-policy.md`; `CONTRIBUTING.md`
  §3 becomes `templates/PR-DESCRIPTION.md`; §4 becomes
  `docs/tier-review-model.md`; §6–§7 become `docs/ticket-lifecycle.md`.
- `DESIGN.md` is named as the adopting project's own design document, since
  this repository has none, and the reference is kept rather than deleted:
  a ticket that advances a design section is a real thing and the template
  should still say so.
- `backlog/` is either described as a fifth directory an adopting project
  may keep, or the sentence is rewritten against the four directories this
  repository documents. The lifecycle publishes four; the template should
  not imply a fifth without saying so.
- The `phase` frontmatter field is kept and marked optional, or removed.
  Whichever, the template and the tickets in this repository agree.
- The worked-example pointer names a file that exists here.

### Falsifier

Per "Retiring a control", for the one rule this ticket touches — that a
published template's references resolve: retired when the templates are no
longer published for copying, at which point their references are internal
to whoever holds them.

## Acceptance criteria

1. AC1: `grep -n "DESIGN.md\|CONTRIBUTING.md\|AGENTS.md\|backlog/"
   templates/` returns only references that name the adopting project's own
   documents in those words.
2. AC2: Every repository-relative path named in a template exists.
3. AC3: The `phase` field is consistent between `templates/TICKET.md` and
   the tickets under `docs/tickets/`.
4. AC4: No template's structure or section list changes.

## Out of scope

- Publishing this repository's equivalents of `DESIGN.md`,
  `CONTRIBUTING.md` or `AGENTS.md`. The policy documents already carry
  their content under other names; this ticket points at those.
- Any change to what a template asks for.

## References

- `DISCLOSURE.md`, "What is published" — the templates' provenance.
- `LICENSE` — "intended to be copied and adapted".
- `docs/ticket-lifecycle.md` — the four directories.

## Notes

Proposed `standard` rather than `trivial`: the change alters instructions an
adopter follows. Under the operative test's `trivial` line as EM-012-001
leaves it the tier would be `trivial`, and EM-007-002 owns that
disagreement; the executor may raise and never lower, so the higher tier is
the one an author can propose without resolving it.

## PR Description

> Leave this section empty when authoring the ticket.
