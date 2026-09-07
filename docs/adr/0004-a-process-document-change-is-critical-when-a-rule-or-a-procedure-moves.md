# ADR-0004: A change to a process document is critical when a rule or a procedure moves

- **Status:** proposed
- **Date:** 2026-09-07
- **Deciders:** maintainer, on the question EM-007-002 reserved
- **Related:** EM-007-002 (this decision); ADR-0002, whose Context sentence
  this narrows in reach; ADR-0001 (adopting the tier model here);
  `docs/tier-review-model.md`, "The operative test" and "Separation of
  duties"; `docs/adr-process.md`, "When to write one"

## Context

Two published statements gave different answers for the same change. The
operative test in `docs/tier-review-model.md` classes as `trivial` a change
where "nothing a program executes and nothing a caller reads as a contract
is touched", and names documentation in the `trivial` row of its tier
table. ADR-0002's Context says "Changes to process documents are
process-surface changes, which the operative test classifies as critical.
So this is not a rare case: on a repository whose content *is* process
documentation, most substantive work is critical tier." A one-word fix to
`docs/ticket-lifecycle.md` was therefore `trivial` by the model and
`critical` by the record.

The conflict was found twice by independent review — of EM-007 (finding 12
of round 2) and of EM-012-001 (finding R2.2 of round 2) — and four tickets
had already been closed on a narrow reading that appeared in no document:
EM-007-001, EM-010-002, EM-012-001-001 and the entries of the batch EM-017,
each recording the reading in its own Notes.

EM-007-002 raised the question and blocked on it under the contributor
policy's §3. Both readings were coherent, so this was not ambiguity; the
question was reserved because it resolves a conflict between a decision
record and the model that record governs, and because one of its answers
removes a control from the party the control is on. Three answers were set
out with their costs, and the maintainer answered on 2026-09-07.

## Decision

A change to a process document is `critical` when it adds, alters or
retires a rule or a procedure, and `trivial` when it does not.
`docs/tier-review-model.md`, "The operative test", states that line in
full — what a rule is, what a procedure is, what the words reach and what
they do not, which party may add to each of those two lists, and the
evidence that would retire the line — and is the authority on it.

ADR-0002's Context sentence keeps its conclusion for every change that
adds, alters or retires a rule or a procedure. What narrows is its reach:
it does not carry process-document changes that do neither. ADR-0002's
Decision — what critical-tier review requires, who may perform it, and what
that reviewer receives — is untouched, and the record keeps `status:
accepted`. It carries a dated annotation pointing here.

The four tickets closed on the narrow reading before it was written down
stand and are not reclassified. Correcting them was a consequence of the
answer that was not chosen.

## Rationale

Three reasons were recorded with the answer.

It matches what four closed tickets already did. The reading was the
repository's practice; the defect was that it lived in four ticket Notes
and in no document a contributor reads before a first edit.

It keeps the batching path usable here. `docs/ticket-lifecycle.md`,
"Batching trivial work", exists so that small changes do not each take a
ticket. Reading ADR-0002's Context as written would have removed that path
on this repository, because nothing here would ever be `trivial`.

The acknowledged cost is accepted rather than denied. The line between
"alters a rule" and "does not" is drawn by the executor, at the moment the
executor would prefer the answer to be `trivial` — ADR-0001's Alternative 3
in a different form. Two things hold it: "Separation of duties", under
which an executor may raise a tier and may never lower one, and the fact
that the line is now in a document, so a `trivial` claim on a
process-document change is checkable by anyone reading the closed ticket.

## Consequences

- **Positive:** the question has one answer, in the document that settles
  which tier a change is, rather than two answers in two documents and a
  third in four ticket Notes.
- **Positive:** ordinary work on this repository — a corrected filename, a
  typo, a dead link — self-merges or batches, as it has been doing.
- **Positive:** the answer carries a falsifier with a stated occasion for
  its check, so the line can be shown wrong rather than argued about.
- **Negative:** the executor draws the line, on its own work, at the point
  where it benefits from the answer. The mitigation is a rule about who may
  move a tier, not a mechanism.
- **Negative:** changes that alter a rule or a procedure on a repository
  made of process documents summon an independent reviewer, and reviews of
  process documents run long. The round cap in `docs/tier-review-model.md`,
  "When review ends", applies.
- **Neutral:** `docs/adr-process.md`, "Decisions about the process are
  themselves ADRs", still says changing the process is a process-surface
  change the operative test classes as `critical`, which now reads wider
  than the model. Reconciling it is EM-007-002-002.
- **Neutral:** one edge of the line is not settled by this record and is
  before the maintainer on EM-007-002: whether correcting a restatement of
  a rule or a procedure, in a document that is not where the question is
  settled, to agree with an unchanged document that is, moves a procedure.
  EM-018-001 is that shape and closed `standard`.

## Alternatives considered

### Alternative 1: ADR-0002's Context governs as written

Every change to a process document is `critical` and summons an
independent reviewer. Rejected on cost: a typo fix in the lifecycle would
cost a review round; the batching path would become unusable here, since
nothing in this repository would ever be `trivial`; and the four tickets
closed on the narrow reading would have been closed at the wrong tier, so
the record would have to say so.

### Alternative 2: Amend ADR-0002 under the amendment-with-record path

Rewrite the Context sentence in place, with a record carrying the old text
and the new, per `docs/tier-review-model.md`, "Retiring a control".
Rejected because that path governs a second-column review finding matching
a rule's stated falsifier, and this was a maintainer's answer to a reserved
question, not a finding. No rule text leaves any document here, and the
sentence amended would be a Context sentence describing a consequence
rather than a rule with a falsifier of its own.

### Alternative 3: Leave the reading in ticket Notes

The status quo: four closed tickets state the narrow reading, and each new
ticket restates it. Rejected because a reading that lives in closed tickets
is not readable by a contributor before a first edit, cannot be held
against a `trivial` claim, and carries no falsifier — which is what let the
conflict survive two independent reviews.

## Migration

No rule text leaves any document. `docs/tier-review-model.md`, "The
operative test", gains the line and its falsifier; ADR-0002 gains a dated
annotation below a horizontal rule, with its text above the rule and its
status unchanged. The four closures stand and are not touched.

Two follow-ups are raised rather than worked here: EM-007-002-001, that the
section's one-line summary carries clauses 1 to 4 and not clause 5, and
EM-007-002-002, that `docs/adr-process.md` still states the wider reading.
