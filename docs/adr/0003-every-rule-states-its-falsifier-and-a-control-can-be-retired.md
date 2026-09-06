# ADR-0003: Every rule states its falsifier, and a control can be retired

- **Status:** accepted
- **Date:** 2026-09-06
- **Deciders:** maintainer, on the executor's implementation of EM-014
- **Related:** EM-014 (this decision); EM-006 (the falsification gate it
  generalises); EM-007 and EM-010 (the review sections it extends);
  `docs/tier-review-model.md`, "Retiring a control"; `docs/adr-process.md`

## Context

The falsification gate asks every test to name the wrong implementation it
rules out. The stopping rule asks every review to say what a converged
review looks like. Until this decision nothing asked a rule what evidence
would retire it, and the consequence was structural: a rule in `docs/` had
no superseded state and no stated condition under which one would apply, so
the control set could only grow. The wave of tickets that diagnosed
monotonic tightening in review (EM-006 to EM-012) was, at the level of the
documents it edits, itself a monotonic tightening — six of seven add to the
brief and say so — and nothing in the repository could have said so.

A reader adopting these documents inherits that property unless it is
changed.

## Decision

Every rule stated in the documents under `docs/` carries a one-line
falsifier introduced by **Retired when:**, or the words **no falsifier
stated** in its place. A second-column review finding (what the change
refuses that honest work needs) that matches a rule's stated falsifier goes
to a retirement ticket, critical tier, which produces a decision record
carrying the rule's text as it stood, the finding that matched, and the
replacement text if any; the rule then leaves the document. Amendment in
place is permitted for a technical match, with the same record. A rule the
change under review itself adds is repaired in the round, not shipped and
retired. The full rule is `docs/tier-review-model.md`, "Retiring a
control".

A ticket raised after EM-014 closed that adds a rule states the rule's
falsifier in its Behaviour section, or it is not ready.

**Exempt tickets.** Rule-adding tickets already in `ready/` when EM-014
closed are not affected; each states the falsifier for the rule it adds when
it is worked, and its pull-request description says so. They are: EM-008,
EM-009, EM-011, EM-012, EM-014-001. EM-001-001, in `blocked/`, adds a gate
script and is treated the same way if it is unblocked. EM-005-001,
EM-006-001, EM-007-001, EM-010-002 and EM-015 in `ready/`, and EM-004 and
EM-013 in `blocked/`, add no rule.

## Rationale

A rule that cannot say what would retire it is unpinned in exactly the sense
a test with a zero red count is unpinned. Stating the falsifier is
uncomfortable in the way naming a test's mutant is uncomfortable, and for the
same reason; the discomfort is the point.

Retirement produces a decision record rather than a parallel directory of
retired rules because `docs/adr-process.md` already requires a decision
record when a workflow rule changes, and one record for one event is the
right number. The first draft of EM-014 proposed a `docs/retired/`
directory; independent review found it duplicated the decision-record
process, and it was dropped.

## Consequences

- **Positive:** the control set can shrink. A second-column finding has
  somewhere to go.
- **Positive:** every rule now carries a claim a reviewer can hold its author
  to, where before it carried nothing.
- **Negative:** one line per rule, and the thinking behind each. The count
  at landing is in EM-014's pull-request description; the cost recurs on
  every rule added afterwards.
- **Negative:** retirement and amendment tickets are critical tier, and
  reviews of process documents run long. The round cap applies.
- **Neutral:** rules whose authors could not state a falsifier say "no
  falsifier stated", which is visible and is meant to be.

## Alternatives considered

### Alternative 1: A `docs/retired/` directory

A parallel record of retired rules beside the decision records. Rejected on
review: the decision-record process already covers a workflow rule changing,
and two records for one event is one too many.

### Alternative 2: Falsifiers only for rules added from now on

Leave the existing rules unmarked. Rejected: the existing rules are the ones
adopted, and the ones most likely to be refusing something nobody has
measured. Marking only new rules would make the obligation look like a
formality.

### Alternative 3: A register of falsifiers reviewed on a cadence

A separate list, checked periodically. Not decided here; EM-014's Out of
scope leaves it for a later ticket with evidence from this one.

## Migration

EM-014 adds the Retired-when lines to every rule in the five rule-bearing
documents under `docs/` and states the counting method and count in its
pull-request description. No rule is retired or amended by EM-014 itself.
