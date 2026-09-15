---
id: EM-007-002-003-001
title: ADR-0004 reads proposed while its decision is in force
status: in-progress
tier: standard
kind: defect
impact: degraded
delivery: maintenance
why: "Without the status matching the merge, a reader of ADR-0004 cannot tell from the record whether the decision it holds binds them, and the decision is the one that sets the tier of every process-document change."
complexity: S
dependencies: []
claimed_by: claude-opus-5
claimed_at: 2026-09-15
blocked_at:
closed_at:
---

# EM-007-002-003-001 — ADR-0004 reads proposed while its decision is in force

## Why this ticket should be worked

The affected outcome is whether a contributor can tell, from a decision
record, that the decision binds them.

`docs/adr-process.md` says a record's status "becomes `accepted` when the
change merges". ADR-0004 reads `status: proposed`, and the commits that
landed it are on the default branch. So the one record that fixes the tier of
every change to a process document — the tier this repository's own tickets
are now worked at — presents itself as a proposal.

The evidence is the record and the history together: `grep -n '^- \*\*Status'
docs/adr/0004-a-process-document-change-is-standard-on-one-pass.md` against
`git log --oneline main -- docs/adr/0004-a-process-document-change-is-standard-on-one-pass.md`.
It was recorded by the round-1 reviewer of EM-007-002-003 as an observation
outside that change, and is raised here under the contributor policy's §4.

This is `degraded` rather than blocking: the decision is followed in practice,
EM-009-001 and EM-007-002-003 both closed under it, and a reader who reads the
body rather than the frontmatter gets the right answer. Deferral is acceptable
while that remains true; it stops being acceptable the first time a
contributor cites the `proposed` status as a reason not to follow the record.

## Context

Raised from the one independent review pass on EM-007-002-003, which recorded
it as an observation rather than a finding because it predates that branch and
is outside its Files.

## Specification

Documentation change only.

### Files

- `docs/adr/0004-a-process-document-change-is-standard-on-one-pass.md`, the
  `Status` line.

### Public surface

N/A — this repository publishes documents.

### Behaviour

- ADR-0004's status states whether the decision is in force, and agrees with
  `docs/adr-process.md`.
- The body of the record and its annotation are untouched.
- Whether other records carry the same mismatch is asked of all of them, not
  only this one, and the answer is stated.

## Acceptance criteria

1. AC1: ADR-0004's status agrees with `docs/adr-process.md` for a record
   whose change has merged.
2. AC2: the status of every record under `docs/adr/` is checked against
   whether its change is on the default branch, and the pull-request
   description states the result per record with the command it was read
   from.
3. AC3: nothing above the annotation's horizontal rule in ADR-0004 changes
   except the status line.
4. AC4: a change to a process document is `standard` on one independent
   review pass, per "The operative test"; the pass is recorded as one row of
   the Review table.

## Out of scope

- Reopening the decision ADR-0004 records, or any part of its body.
- Any change to `docs/adr-process.md` itself, including whether the status
  transition should be mechanically enforced.

## References

- `docs/adr-process.md` — the status transition this record does not follow.
- `docs/adr/0004-a-process-document-change-is-standard-on-one-pass.md`.
- EM-007-002-003, Risks / follow-ups — where this was routed.
- EM-007-002 — the ticket that landed ADR-0004 and closed without the
  transition.

## Notes

The same close step was taken correctly on ADR-0005, which EM-009-001 moved
from `proposed` to `accepted` in its closing commit on 2026-09-15. That is one
record done right and one done wrong, which is what AC2 asks the sweep to
settle rather than assume.

## PR Description

> Leave this section empty when authoring the ticket.
