---
id: EM-007-002-003-001
title: ADR-0004 reads proposed while its decision is in force
status: done
tier: standard
kind: defect
impact: degraded
delivery: maintenance
why: "Without the status matching the merge, a reader of ADR-0004 cannot tell from the record whether the decision it holds binds them, and the decision is the one that sets the tier of every process-document change."
complexity: S
dependencies: []
claimed_by: claude-opus-5
claimed_at: 2026-09-15
closed_at: 2026-09-15
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

### Ticket
EM-007-002-003-001 — ADR-0004 reads proposed while its decision is in force.

### Tier
`standard`, on one independent review pass. "The operative test" names a
decision record under `docs/adr/` as a process document, which fixes the tier
there; it is not the executor's to raise or lower. The pass ran against
08b4b88 and is row 1 of the Review table.

### Summary
`docs/adr-process.md` says a record's status "begins `proposed` and becomes
`accepted` when the change merges". ADR-0004's commits are on the default
branch and its status read `proposed`, so the record that fixes the tier of
every process-document change presented itself as a proposal. One line
changes.

### Acceptance criteria
- [x] AC1: ADR-0004's status agrees with `docs/adr-process.md`. The sentence
  relied on is in "Structure": "Status begins `proposed` and becomes
  `accepted` when the change merges." ADR-0004's change is on `main`, so
  `accepted` is what that sentence requires, and `accepted` is what the record
  now reads. The rule is quoted from the document rather than asserted: the
  reviewer checked it is there, unqualified, and that no rule anywhere in
  `docs/` bars a late transition.
- [x] AC2: the status of every record under `docs/adr/` is checked against
  whether its change is on the default branch. Read with `grep -m1 '^- \*\*Status:\*\*' <path>`
  and `git log --oneline main -- <path>`, both run after 08b4b88 against
  `main` as it stood at that commit's parent:

  | Record | Status before this change | Commits on `main` | Agrees? |
  |---|---|---|---|
  | ADR-0001 | accepted | yes | yes |
  | ADR-0002 | accepted | yes | yes |
  | ADR-0003 | accepted | yes | yes |
  | ADR-0004 | **proposed** | yes | **no — the mismatch** |
  | ADR-0005 | accepted | yes | yes |

  ADR-0004 was the only mismatch. One nuance, so the sweep is not read as more
  than it is: ADR-0001 and ADR-0002 pass this test for a different reason than
  ADR-0003 and ADR-0005 do. The first two were created `accepted` and never
  passed through `proposed`, which ADR-0001's own 2026-09-06 annotation
  records and explains. The second two were created `proposed` and transitioned
  on close. ADR-0004 is of the second kind and its transition was simply
  missed.
- [x] AC3: nothing above the annotation's horizontal rule changes except the
  status line. `git show 08b4b88` is one file, one hunk, one line: `- **Status:**
  proposed` becomes `- **Status:** accepted`. Date, Deciders and Related are
  context lines. Nothing below the rule changes and no second file is touched.
- [x] AC4: one independent review pass, run against 08b4b88 by an agent that
  did not perform the work and did not receive the executor's reasoning,
  recorded as row 1 of the Review table below. It returned two must-fixes over
  three findings; one is repaired here and one is routed.

### Falsification
N/A for a behavioural claim — this repository publishes documents and runs no
suite. Per criterion, what a reader does differently: a contributor who opens
ADR-0004 to find out what tier their process-document change takes reads a
decision that is in force, rather than one presenting itself as a proposal
they might not have to follow.

For the review finding repaired, per the contributor policy's §6:

- R1.1 — class: **which acceptance criteria does this change assert as met
  without the evidence living in the tree?** AC2's sweep is the instance: the
  description was unwritten at 08b4b88 and the commit message carried only the
  aggregate "the only mismatch", with no pair per record, no command and no
  baseline. The question was asked of all four criteria. Siblings:
  - **AC2** — the instance. Repaired: the table above gives the pair per
    record and names the two commands and the commit they were run after.
  - **AC1** — checked. It asserted agreement with `docs/adr-process.md` without
    quoting the sentence relied on, which is the same defect one degree
    milder: a reader could not check the rule without going to find it.
    Repaired in the same round; AC1 now quotes it.
  - **AC3** — checked and sound. It names `git show 08b4b88` and states what
    that command shows, which a reader can run.
  - **AC4** — checked and sound; it is discharged by the pass whose row is
    below, and the row is its evidence.
  What a reader does differently: a reader auditing the sweep re-runs two named
  commands over five files and gets the same table, instead of having to take
  an aggregate on the executor's word.
- R1.3 — note. Repaired in the round; a note carries nothing under §6 as
  EM-009-001 narrowed it. The distinction it asked for is in AC2 above and in
  the precedent paragraph below.

**On ADR-0001's annotation, which declines to rewrite a status.** It says of
ADR-0001 and ADR-0002: "The two are left as they stand rather than edited to
`proposed` and back. Rewriting a status after the fact would be the same shape
of fabrication this record rejects for tickets." That passage is about records
created `accepted`, where writing `proposed` would assert a state that was
never true. This change is the other case: ADR-0004 was created `proposed`,
the transition its own process document requires was simply late, and writing
`accepted` asserts nothing that is not true. The precedent is in the tree
twice — ADR-0003 moved to `accepted` at 9b5f972, in EM-014's close commit, and
ADR-0005 at 3fb7c37, in EM-009-001's — each a one-line change in a close
commit with no decision record. This change follows those and does not
contradict ADR-0001's annotation.

### Routed, not repaired
R1.2 is a must-fix the reviewer recorded and this ticket does not repair.
ADR-0004's 2026-09-15 annotation opens "the text above the horizontal line is
unchanged, and the status is unchanged", and this change alters the status
above that rule on the same date. The sentence has a narrow reading under
which it stays true — that annotation did not change the status — and a broad
one under which it is now false, and the file supports neither over the other.

The remedy lies inside two limits this ticket records: Behaviour, "The body of
the record and its annotation are untouched", and Out of scope, "any part of
its body". Under the second condition of "When review ends" it therefore goes
to a ticket that owns it, raised because none existed: **EM-007-002-003-002**.
That one must-fix is discharged by raising it.

### Out of scope (per ticket)
Confirmed; nothing here exceeds it.
- The decision ADR-0004 records, and any part of its body — untouched. The
  status line sits in the record's header, not its body, and AC3's diff shows
  nothing else moved.
- `docs/adr-process.md`, including whether the transition should be
  mechanically enforced — untouched.

### How to verify
1. `grep -n '^- \*\*Status:\*\*' docs/adr/*.md` — five records, all `accepted`.
2. `for f in docs/adr/*.md; do echo "$f $(git log --oneline main -- $f | wc -l)"; done`
   — every record has commits on the default branch, which is AC2's test.
3. `git show 08b4b88` — one file, one hunk, one line, which is AC3.
4. `sed -n '/Status begins/p' docs/adr-process.md` — the sentence AC1 relies on.

### Risks / follow-ups
- **A status that should transition on close has no site that goes red.**
  ADR-0003 and ADR-0005 transitioned in their close commits and ADR-0004 did
  not, and nothing caught it for five days; it was found by a reviewer reading
  an unrelated change. That is one instance of a missing check, and "A rule
  needs a second instance" bars writing a rule on one, so it is recorded here
  rather than raised. A second would make the case for the close procedure
  naming the step, or for the figure having a site that fails.
- The two kinds of record — created `accepted`, and created `proposed` and
  transitioned — pass AC2's test for different reasons, and nothing in
  `docs/adr-process.md` says the first kind is allowed. ADR-0001's annotation
  explains why those two exist and why they were not rewritten, which is the
  record a reader needs; whether the process document should say it is a
  question this ticket does not open.

### Review
One independent review pass, per "The operative test" for a change to a
process document. No second pass is taken.

| Round | Must-fix | Where (rules / lists / documents / tests) | Inside previous round's fix | Repaired by |
|---|---|---|---|---|
| 1 | 2 (of 3 findings) | documents: AC2's per-record sweep is asserted in the commit message as an aggregate and lives nowhere in the tree, so the criterion's evidence cannot be checked (must-fix); ADR-0004's 2026-09-15 annotation says the status is unchanged while this change alters it above that rule on the same date (must-fix, routed to EM-007-002-003-002); the change edits a status after the fact and says nothing about ADR-0001's annotation, which declines to, leaving a reader unable to tell precedent from contradiction | — | this commit |

Derived from the row and not asserted beside it: two must-fixes over one
review round, of which one is repaired here and one is discharged by raising
EM-007-002-003-002. Round 1 has no round before it, so its inside-previous-fix
cell reads `—` and no line is uncountable.

- R1.1 · permits · must-fix · `docs/ai-contributor-policy.md` §6, "Every acceptance criterion met and demonstrated in the pull-request description, with evidence", and AC2's own "with the command it was read from" · the sweep existed only as an aggregate in a commit message, with no pair per record, no command and no baseline, so AC2's evidence was unverifiable from the change — remedy: write the per-record table into the description and name the commands and the commit they were run after; cost, if the remedy tightens a control: none, it supplies evidence the criterion already names; inside previous fix: —
- R1.2 · permits · must-fix · `docs/adr/0004-...md`, the 2026-09-15 annotation's preamble · it states that the status is unchanged, and this change alters the status above that rule on the same date, leaving the record asserting both with nothing to order them — remedy: a clause in that preamble naming the later transition, or a new dated annotation below its own rule; routed to EM-007-002-003-002 under the second condition of "When review ends", since the remedy lies inside this ticket's Behaviour and Out of scope; cost, if the remedy tightens a control: none; inside previous fix: —
- R1.3 · permits · note · `docs/adr/0001-...md`, the 2026-09-06 annotation, "Rewriting a status after the fact would be the same shape of fabrication this record rejects for tickets" · the change edits a status after the fact and distinguishes its case from that passage nowhere, so a reader finding the annotation cannot tell precedent from contradiction — remedy: a sentence distinguishing the created-`accepted` case from the late transition, naming 9b5f972 and 3fb7c37; cost: none; inside previous fix: —

The reviewer found nothing in the second column and recorded that as an
answer: the change is a single-token status flip that adds no rule, no list
entry and no refusal, removes no path honest work uses, and leaves the record
open to supersession under `docs/adr-process.md`. No tightening occurred, so
no cost line is owed under "A tightening states its cost", and none of the
first-column remedies adds a control either.

### Definition of Done (all tiers)
The four machine checks do not apply to a repository that publishes documents
and runs no suite; the falsification gate is discharged above, with N/A for
the behavioural claim and a class line for the must-fix repaired. Every
measured figure names its baseline in the same sentence and is read from the
command named beside it. The independent pass a process-document change takes
has run and is recorded.
