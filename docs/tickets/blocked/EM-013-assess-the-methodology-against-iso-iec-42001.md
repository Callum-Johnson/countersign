---
id: EM-013
title: Assess the methodology against ISO/IEC 42001
status: blocked
tier: standard
complexity: L
dependencies: [EM-002]
claimed_by: claude-fable-5-1
claimed_at: 2026-09-06
blocked_at: 2026-09-06
---

# EM-013 — Assess the methodology against ISO/IEC 42001

## Context

ISO/IEC 42001:2023 is the management-system standard for artificial
intelligence: the clause structure an organisation is audited against when it
claims to govern its AI responsibly, plus an annex of reference controls.

This repository describes an AI governance system built from first principles
on a private project — a written contributor policy, a ticket lifecycle with an
enforced invariant, tiered review with separation of duties, decision records,
machine-checked gates. None of it was built with the standard open.

That makes the comparison worth doing honestly rather than as a compliance
exercise. Where the methodology already satisfies a clause, that is evidence
the practice is sound. Where it does not, that is a real gap in how AI agents
are governed here, and it belongs on this board as work. Where the standard
asks for something that makes no sense at the scale of one maintainer and a
fleet of agents, saying so plainly is more useful than pretending to comply.

## Specification

Produce a clause-by-clause assessment of this repository's documented
practice against ISO/IEC 42001, and raise a ticket for every material gap.

### Files

- `docs/assessments/iso-iec-42001.md` — the assessment
- `docs/tickets/ready/EM-013-NNN-*.md` — one ticket per material gap, as
  lineage children of this ticket

### Behaviour

- Every clause of the main body (4 through 10) and every control in the
  annex receives one of exactly four verdicts: **met**, **partially met**,
  **not met**, or **not applicable** — with one or two sentences of reasoning
  and a link to the artifact that evidences it.
- "Not applicable" requires a stated reason. Scale is a legitimate reason;
  inconvenience is not.
- Verdicts are conservative. Where the practice does something similar but
  not the thing the clause asks for, that is *partially met*, not *met*.
- Each *not met* or *partially met* verdict that would change how agents are
  governed here is raised as a lineage child ticket. Gaps that would not
  change anything are recorded in the assessment and left there.
- A summary table at the top gives the counts per verdict, so a reader can
  see the shape in five seconds.

### Constraint

**The standard's text is copyrighted and is not reproduced.** Clauses and
controls are referenced by number and by a short paraphrase of what they ask
for, in this repository's own words. No clause text, no control text, no
annex tables. The same rule this repository applies to a third party's game
rules applies to a standards body's standard.

## Acceptance criteria

1. AC1: `docs/assessments/iso-iec-42001.md` exists and covers clauses 4–10
   and every annex control, each with a verdict from the four allowed.
2. AC2: Every verdict cites an artifact in this repository, or states that
   none exists.
3. AC3: Every *not applicable* verdict states its reason.
4. AC4: Every material gap has a lineage child ticket in `ready/`, linked
   from the assessment.
5. AC5: A search of the assessment for any sentence of the standard's text
   returns nothing. Paraphrase only.
6. AC6: The summary table's counts match the body.

## Out of scope

- Implementing the gaps. Each is its own ticket.
- Claiming or implying certification, conformity, or readiness for audit.
  This is a self-assessment by the author of the thing being assessed, and
  the document says so in its first paragraph.
- Assessing the private projects the methodology came from. Only what is
  published here is in scope, because only that can be checked by a reader.
- Mapping to any other framework. If that is wanted later it is a separate
  ticket, and the four-verdict structure should be reused.

## References

- ISO/IEC 42001:2023 — by purchase; not held in this repository
- `docs/ai-contributor-policy.md`, `docs/tier-review-model.md`,
  `docs/ticket-lifecycle.md`, `docs/quality-gates.md`, `docs/adr-process.md`
- ADR-0001, ADR-0002
- `DISCLOSURE.md` — the reproduction rule this ticket's constraint extends

## Notes

The interesting output is not the *met* column. A methodology built without
the standard that turns out to satisfy most of it says something about the
standard and something about the methodology. The *not met* column, written
without flinching, is what makes the *met* column believable.

Expect the management-context clauses (leadership, roles, resourcing,
competence) to be where a one-maintainer repository looks thinnest. Do not
pad them. ADR-0002 is the model: name the constraint, decide what to do about
it, record it.

**BLOCKER (2026-09-06):** the pre-flight checklist in contributor policy §7
requires the executor to have read every external reference the ticket
cites. The one reference that matters is held "by purchase; not held in this
repository", and the executor cannot read it.

The executor could assess against its own recollection of the standard's
clause structure — the seven main-body clauses and the Annex A control
families are widely paraphrased — but a clause-by-clause verdict written
against a paraphrase the executor has not checked is the "proceed with a note
saying you assumed something" that §3 forbids, and whether that is acceptable
here is the maintainer's decision, not the executor's.

To proceed the executor needs one of:

1. The maintainer's authorisation to assess against the executor's own
   paraphrase of clauses 4–10 and each Annex A control, with the maintainer
   checking every clause and control number against the purchased text
   before the ticket closes, and the assessment's first paragraph saying that
   is how it was produced; or
2. A maintainer-written input file — clause or control number and one line
   of paraphrase each, in the maintainer's own words — which the executor
   assesses against. This also gives AC5 a concrete thing to test: the
   assessment reproduces nothing that is not in that file.

The second is the better artifact, since the paraphrase then has one author
who has read the standard.
