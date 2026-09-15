# ADR-0004: A change to a process document is standard, on one pass

- **Status:** proposed
- **Date:** 2026-09-10
- **Deciders:** maintainer, on the question EM-007-002 reserved
- **Related:** EM-007-002; ADR-0002, whose Context sentence this narrows in
  reach; ADR-0003, whose Consequences name a tier this changes; ADR-0001
  (adopting the tier model here); `docs/tier-review-model.md`, "The
  operative test", "The tiers" and "Separation of duties";
  `docs/adr-process.md`, "When to write one" and "Decisions about the
  process are themselves ADRs"

## Context

Two published statements gave different answers for the same change. The
operative test in `docs/tier-review-model.md` classed as `trivial` a change
where "nothing a program executes and nothing a caller reads as a contract
is touched" and named documentation in the `trivial` row of its tier table.
ADR-0002's Context said "Changes to process documents are process-surface
changes, which the operative test classifies as critical." A one-word fix to
`docs/ticket-lifecycle.md` was `trivial` by the model and `critical` by the
record. Independent review found the conflict twice — of EM-007 (finding 12
of round 2) and of EM-012-001 (finding R2.2 of round 2) — and four tickets
had closed on a narrow reading that appeared in no document: EM-007-001,
EM-010-002, EM-012-001-001 and the entries of the batch EM-017.

EM-007-002 raised the question and blocked on it under the contributor
policy's §3, since one available answer removes a control from the party
the control is on. The maintainer's first answer, on 2026-09-07, drew a line
through process-document changes: `critical` where a rule or a procedure is
added, altered or retired, `trivial` otherwise. Writing that line down took
four independent review passes on 2026-09-07 and 2026-09-08 — rows 1 to 4
of EM-007-002's Review table — the last of them ordered past the round cap,
and each pass found defects in the previous pass's repair of the line. The
line never landed.

On 2026-09-10 the maintainer answered again, and this record carries that
answer. The finding behind it: the raise-never-lower rule together with a
`critical` default drove every documentation ticket into the full review
loop — EM-024 ran four independent passes on prose — and the loop's cost on
documents was disproportionate to what it caught.

## Decision

A change to a process document is **`standard`**: one independent review
pass, closing on that pass. **The executor may not raise it** to `critical`.
It is neither `trivial` by the operative test nor `critical` by ADR-0002.

`docs/tier-review-model.md`, "The operative test", states the rule in full —
what a process document is, what the one pass consists of, that the tier is
not raised, and the evidence that would retire it — and is the authority on
it. The pass is an independent reviewer in ADR-0002's sense, recording in
the two columns of "What a review reports" as one row of the Review table;
what changes is that there is one, and the ticket closes on it.

This is a narrowing of ADR-0002's reach. Its Context sentence carried every
process-document change to `critical`; it now carries none. What ADR-0002
decides — what critical-tier review requires, who may perform it, and what
the reviewer receives — is untouched, and that record keeps `status:
accepted` with a dated annotation pointing here.

**Text amended under this decision.** Per `docs/adr-process.md`, "When to
write one", a workflow rule changing carries the text as it stood, the
finding, and the text that replaces it. The finding is the one in Context
for every line below.

- `docs/tier-review-model.md`, "The operative test", the `trivial` clause.
  Stood: "`trivial`: documentation, comments, ticket files, data no program
  loads." Now: "`trivial`: documentation other than a process document,
  comments, ticket files, data no program loads." The one-line summary gains
  the sentence "A process document is `standard`, on one pass, whatever the
  answer."
- `docs/tier-review-model.md`, "The tiers". Stood: the `trivial` row's
  "Documentation, comments, data no program loads, ticket edits" and the
  `standard` row's "None; author self-merges after a complete PR description
  with evidence per criterion". Now: the `trivial` row reads "Documentation
  other than a process document", and the `standard` row names every change
  to a process document and gives it one independent review pass, closing
  on it.
- `docs/tier-review-model.md`, "Separation of duties". Stood: "**The
  executor may raise** it … and records a one-line reason." Now: the same,
  followed by "A change to a process document is the exception: its tier is
  `standard` and is not raised."
- `docs/tier-review-model.md`, "Retiring a control". Stood: "That ticket is
  a **retirement ticket**, critical tier under the process-surface clause of
  the operative test." Now: "a **retirement ticket**, `standard` on one
  independent pass, as every change to a process document is".
- `docs/adr-process.md`, "Decisions about the process are themselves ADRs".
  Stood: "Changing the process is a process-surface change, which the
  operative test classifies as `critical`, which means it needs a second
  reviewer." with **Retired when:** "the tier model ceases to class the
  process surface as `critical`". That falsifier is matched by this decision
  and the rule is amended in place with this record; the match is
  technical — one tier word in the second sentence, the first sentence and
  the argument unchanged. Now: "Changing the process is a change to a
  process document, which the operative test classes as `standard` with one
  independent review pass, which means it still has a reader who did not
  write it." with **Retired when:** "the tier model ceases to give a change
  to a process document an independent pass".
- `docs/adr-process.md`, "What 'a workflow rule changes' reaches". Stood:
  "a rule added to a process document is a process-surface change under the
  operative test either way." Now: "a process-document change under the
  operative test either way, `standard` on one independent pass."
- `templates/PR-DESCRIPTION.md`, the `### Review` header. Stood: "Critical
  tier only; write `N/A` otherwise." Now: "Critical tier, and a change to a
  process document; write `N/A` otherwise." — the one pass is recorded as
  one row of the Review table, and a header that refused the section to
  every tier but `critical` discarded it. Found by the one pass on
  EM-007-002 (R5.1).
- ADR-0002, Context. Stood: "Changes to process documents are process-
  surface changes, which the operative test classifies as critical." Not
  amended — an accepted record is not rewritten — but annotated: the
  sentence's reach is narrowed to nothing, and its conclusion is replaced by
  the rule above.

The closures made before this record — the four `trivial` closures named in
Context, EM-018-001's `standard` closure, and every `critical` closure of a
process-document change — stand and are not reclassified. The decision binds
from 2026-09-10 forward.

## Rationale

The cost was measured before the decision, not predicted. Under a `critical`
default with raise-never-lower, no process-document change could ever be
anything but `critical`, since the only party who could lower it was the
reviewer the tier summoned. On a repository made of process documents that
put every substantive ticket into the multi-round loop, and the loop's
record on prose is the evidence: EM-007-002's own four passes, EM-024's four,
each pass finding defects inside the previous pass's repair.

One pass keeps what the loop was for — a reader who did not write the change
checks it against the ticket — and drops what the loop cost. Fixing the tier
removes the occasion on which an executor chose: the first answer's line
was drawn by the executor at the moment it would prefer `trivial`, which is
ADR-0001's Alternative 3 in another form, and every pass on it found the
line moved. A tier nobody moves has no such occasion.

The rule states its falsifier in the terms the tier model uses for the
`trivial` line: the boundary is between a process document and what a
program executes or a caller reads as a contract, and a change closed on
one pass that turns out to have crossed it is the evidence that the boundary
is in the wrong place.

## Consequences

- **Positive:** the question has one answer in the document that settles
  which tier a change is, and the same answer in every document that
  restates it.
- **Positive:** a process-document change costs one independent pass; the
  round cap, the per-round loop and the repairs-of-repairs signal have no
  application to it.
- **Positive:** the executor has no tier decision to make on a
  process-document change, so the failure the first answer's four passes
  kept finding — an executor lowering while believing it had not — has no
  site.
- **Negative:** a rule change with a defect the one pass misses ships with
  it. The falsifier counts the case where the defect is of the kind the tier
  exists to catch; a defect in prose that changes nothing a program executes
  is the cost accepted.
- **Negative:** `trivial` no longer reaches any process document, so a typo
  in `docs/ticket-lifecycle.md` takes a ticket and a pass, and the batch path
  of `docs/ticket-lifecycle.md`, "Batching trivial work", does not carry it.
- **Negative:** the `standard` row of "The tiers" now carries two review
  requirements, self-merge for code and one pass for a process document.
  The row says which applies to what.
- **Neutral:** clause 5 of the operative test still names "a change to the
  review model itself"; the review model is a process document and the
  paragraph beneath the test decides its tier. The clause's words are
  unchanged, being outside EM-007-002's scope.
- **Neutral:** ADR-0003's Consequences bullet naming retirement tickets as
  critical tier is annotated, not rewritten.

## Alternatives considered

### Alternative 1: ADR-0002's Context governs as written

Every change to a process document is `critical` and enters the full loop.
Rejected on the measured cost in Context. It also makes the batch path
unusable here, since nothing in this repository would ever be `trivial`.

### Alternative 2: a `critical`/`trivial` line through process-document changes

The answer of 2026-09-07: `critical` when a rule or a procedure is added,
altered or retired, `trivial` otherwise, with the executor drawing the line
and permitted only to raise. Replaced before it landed. Four passes found
the line's text defective on each attempt, most of the defects inside the
previous repair, and the executor twice lowered while claiming to tighten;
the line put the tier decision on the party who benefits from it, and
mitigated that with the very raise-never-lower rule that produced the loop.

### Alternative 3: every process-document change is `trivial`

Self-merged, no reader. Rejected: a policy document published as evidence is
not `trivial`, which is ADR-0002's Alternative 2 and stands; a rule change
nobody but its author has read is the silent change `docs/adr-process.md`
says is not a control.

### Alternative 4: `standard` as the row already reads — self-merge

Rejected for the same reason as Alternative 3; the one pass is what makes
`standard` honest for a document that binds contributors.

## Migration

No rule text leaves any document. The lines amended are listed in Decision
with their old and new text. ADR-0002 and ADR-0003 gain dated annotations
below a horizontal rule, with their text above the rule and their status
unchanged. The record written under the first answer, which this file
replaces, never merged; its content is in EM-007-002's history at a0adb0b.
It was rewritten and renamed in place rather than kept as `superseded` or
marked `withdrawn`, because both of those statuses are for a record that
was published and this one never left its branch — `docs/adr-process.md`
does not say what to do with a `proposed` record replaced before it merges,
and this sentence records the choice made.

No closed ticket is reclassified. EM-007-002 itself is worked under this
decision, at `standard`, on one pass. EM-007-002-002, which was to reconcile
`docs/adr-process.md` with the first answer, is mooted by the amendment
above and closed unworked; EM-007-002-001, that the operative test's
one-line summary omits clause 5, stands for a CI configuration change and a
schema migration and is amended here for a process document.

---

## Annotation — added 2026-09-15 under EM-007-002-003

> Not part of the decision as recorded. The text above the horizontal line
> is unchanged, and the status is unchanged.

The Consequences bullet beginning "clause 5 of the operative test still names
'a change to the review model itself'" describes the clause as it stood at
this record's date, and both halves of its last two sentences have since
stopped holding. EM-007-002-003 amended the clause on 2026-09-15. It stood as:

> 5. **Process surface.** A schema migration, a CI configuration change, or a
>    change to the review model itself.

and now reads:

> 5. **Process surface.** A schema migration or a CI configuration change. A
>    change to the review model itself is a change to a process document, and
>    the paragraph **A change to a process document** below, and the tier it
>    states, decide that; this clause does not.

So the clause no longer names a change to the review model, and its words are
no longer unchanged. The decision this record holds — that a change to a
process document is `standard` on one independent pass — is untouched, and the
amendment brings the clause's words into agreement with it rather than
altering it.
