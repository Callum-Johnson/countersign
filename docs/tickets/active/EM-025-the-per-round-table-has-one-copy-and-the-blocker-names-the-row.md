---
id: EM-025
title: The per-round table has one copy, and the blocker names the row
status: in-progress
tier: standard
complexity: M
dependencies: []
claimed_by: claude-fable-5-1
claimed_at: 2026-09-10
---

# EM-025 — The per-round table has one copy, and the blocker names the row

## Context

Between 2026-09-06 and 2026-09-09, by the dates the records themselves
carry, five tickets across the control-plane project and this repository
ran between three and eight independent review passes each — OMN-024,
OMN-022-003, OMN-022-002, OMN-020-001 and EM-024 — and the maintainer asked
whether the difficulty was the code or the method of keeping the record. This
ticket is the part of the answer that survived being refuted three ways, and
it is one rule.

Every figure below names the command that produced it and the commit it was
read at. Three of the five records are on branches that must be pushed before
a fresh clone can reproduce them; Notes says which.

### What the review rounds found, in total

Must-fixes per record, read from each record's `### Review` section — the
count of `- R<n>.<k> ·` bullets graded must-fix by the marker that record
uses, cross-checked against each record's own derived total:

```sh
extract(){ awk '/^### Review/{r=1;next} !r{next} /^- (\*\*)?R[0-9]+\.[0-9]+ ·/{if(b!="")print b;b=$0;next} /^  [^ ]/&&b!=""{sub(/^  /,"",$0);b=b" "$0;next} {if(b!="")print b;b=""} END{if(b!="")print b}'; }
```

| Record | Read at | Must-fixes |
|---|---|---|
| OMN-024 | `7ab004a` | 17 |
| OMN-022-003 | `4e1b963` | 8 |
| OMN-022-002 | `412e714` | 15 |
| OMN-020-001 | `412e714` | 11 |
| EM-024 | `c6ee58b` | 8 |

Whether a must-fix's remedy touches a source or test file, or only the
record's own text, **depends on how a docstring in a source file is graded**:
three independent readings of the same fifty-nine remedies put between
twenty-eight and forty on the code side, and the whole of the disagreement is
sentences that live in `src/` or `tests/` and describe the tree — a count in
a test's docstring, a claim about what a grep returns in a module's. That
boundary is EM-024's, not this ticket's: a sentence describing the tree has
its determiner in the tree wherever the sentence sits, and the rule landed at
`d669ead` already reaches it. What this ticket takes from the fifty-nine is
narrower.

### The one shape that is Countersign's own

`docs/tier-review-model.md`, "When review ends", says at the round cap that
*the per-round table is appended to the ticket file under the `BLOCKER:`
comment*. The records obey it. Copies of the table's header row, by
`grep -c '^| Round | Must-fix |'`: OMN-024 2, OMN-022-003 4, OMN-022-002 4,
OMN-020-001 1, EM-024 1 — one copy per block plus the one in the description.

Two things then happen, each recorded by the record it happened in.
OMN-022-002's round-13 executor found the two copies **had diverged by a
row** — the description's copy carried row 12 and the blocker's did not — and
restored it, recording the restoration at line 813 of the record at
`412e714`. EM-024's round-4 review found a phrase corrected in one sub-section
and its twin left standing in another the executor had not read, recorded at
lines 327–328 of the record at `c6ee58b`. The read-whole rule at
`tier-review-model.md:354` exists for this and was in force for both; a copy
that must be found by reading is a copy that will be missed, and a rule that
mandates the copy guarantees the reading.

EM-024's rule says a number has one site and every other mention names the
site. The per-round table is the site for every number in it. The standing
text at :338 then requires a second site. That is the contradiction this
ticket resolves, and it is the whole of what it does.

## Specification

One rule, amending one sentence, in `docs/tier-review-model.md` under "When
review ends".

### The rule

**The per-round table has exactly one copy in the ticket file, in the
`## PR Description`'s Review section.** A `BLOCKER:` comment written at the
round cap, a discharge note, or any summary that needs what the table holds
**names the row** — "row 4, three must-fixes, all inside the previous fix" is
written as "see row 4" — and carries no figure the table determines. The
sentence at :338 that appends the table under the blocker is replaced by one
that points at it. Finding lines follow the same rule: one copy, in the
Review section, and the blocker names R<n>.<k> rather than restating it.

What the rule does not do: it does not shorten the blocker beyond the copy,
does not touch what the template requires per finding — a finding still says
whether it sits inside the previous round's fix, because that is the
template's field and not a restatement — and asks nothing retrospective, as
EM-024's section does not. Records written before it are read under the rule
that was in force.

**Retired when:** over the next fifty closed critical-tier tickets on an
adopting project, a blocker that names a row rather than copying the table is
found by the round that reads it to have named the wrong row, more than once
— the pointer would then be no better a site than the copy was. Fifty is the
population EM-024's section uses, chosen there for the same reason: the
evidence is a handful of records on two projects.

### Files

- `docs/tier-review-model.md`, "When review ends" — the sentence at :338, and
  the index if the section's summary line changes
- `docs/ai-contributor-policy.md` §3 — the `BLOCKER:` guidance, which says
  what a blocker carries; one clause pointing at the row
- `templates/PR-DESCRIPTION.md`, `### Review` — one sentence: the table
  appears once
- `docs/ai-contributor-policy.md` — the map, if the tier model's row changes;
  the map/index same-commit rule at :50–55 applies

### Public surface

A blocker written at the cap is read by the maintainer before anyone else.
Under this rule they read one table, in one place, and a note that says which
rows to look at. That is the whole user-visible change.

### Behaviour

- The rule states what a **reader** does differently: a reviewer meeting a
  second copy of the per-round table records it as a finding on its face,
  with no measurement, the way EM-024's section treats a number in a second
  place.
- **This ticket's own record obeys the rule and EM-024's from its first
  commit**: its table appears once, its blocker if any names rows, and every
  number in it names its command and commit. A reviewer finding it in breach
  grades that must-fix, as EM-024's reviewers did in each of its rounds.
- No decision record is owed: this amends a sentence under an existing
  decision, per `docs/adr-process.md`. If the executor concludes otherwise,
  it says why.

## Acceptance criteria

1. AC1: `docs/tier-review-model.md` "When review ends" no longer appends the
   table under the blocker and instead names the row; `grep -c 'appended to
   the ticket file under the' docs/tier-review-model.md` returns 0.
2. AC2: the rule carries a `Retired when:` line naming its population.
3. AC3: `templates/PR-DESCRIPTION.md` `### Review` states that the table has
   one copy, and §3's blocker guidance points at the row.
4. AC4: this ticket's own file carries the header `| Round | Must-fix |` at
   most once — `grep -c '^| Round | Must-fix |' <this file>` returns 0 or 1
   — at every commit on its branch.
5. AC5: the map and the index are consistent with the amended section in the
   same commit, per `docs/ai-contributor-policy.md:50–55`.

## Out of scope

- A ceiling on the record's length. It was drafted and refuted: OMN-022-003
  at 2,366 lines carried one record must-fix and OMN-024 at 2,919 carried
  the most, so length does not predict the defect; restatement does, and
  that is what this rule addresses.
- Citing figures from harness artefacts rather than transcribing them. It
  was drafted and refuted: `docs/quality-gates.md:163` requires the red count
  beside the claim in the description, and a committed file is not a site
  that goes red under EM-024's own text at :336. The observation that the
  control-plane harness writes a per-mutant table nobody cites, and that its
  coverage has no `--cov-report`, is a control-plane tooling note and is
  raised there, not here.
- Pinning `path:line` citations to a commit. It was drafted and refuted: a
  citation true at its commit and unresolved at head is worse than useless
  to a reviewer, and EM-024 already treats a line number as a number
  determined elsewhere. The measurement stands — of OMN-022-002's ten
  earliest distinct citations into `src/` and `tests/`, four resolve to what
  they name at `412e714` and six do not, all six into `transitions.py` and
  `manager.py` — and goes to EM-024 as its class, not here as a rule.
- Repairing the five records.

## References

- `docs/tier-review-model.md:338` — the sentence amended
- `docs/tier-review-model.md:354` — the read-whole rule, which the copy
  defeats
- `docs/quality-gates.md`, "A number determined elsewhere has one site that
  goes red", at `d669ead` — the rule this one applies to a table
- EM-024 at `c6ee58b`, lines 327–328; OMN-022-002 at `412e714`, line 813 —
  the two instances
- `templates/PR-DESCRIPTION.md`, `### Review`

## Notes

Raised on 2026-09-10. Three drafts of this ticket's Specification were
refuted before this one: a four-rule version carrying a record ceiling, an
artefact-citation rule and a pinned-citation rule fell to the standing gate
text, to EM-024's own wording, and to its own evidence table. What survived
is the one rule whose two instances are Countersign's own mandate producing
the defect.

**Before this ticket can be worked from a fresh clone**, three refs it reads
must be on `origin`: `EM-024-a-count-in-prose-has-no-falsifier` at `c6ee58b`
(never pushed), `OMN-024-the-gates-are-the-branchs-gates` at `7ab004a`
(origin is at `e8aca29`), and
`OMN-022-003-a-workspace-row-outlives-the-directory-a-person-removed` at
`4e1b963` (origin is at `4e4493e`). The two `412e714` records are on the
control-plane `main`. The executor confirms all five with
`git ls-remote --heads origin` before measuring anything.

**Tier.** Proposed `standard`. EM-007-002's open question applies as to every
documentation ticket; the executor may raise and never lower.

**Second instances**: OMN-022-002's diverged copies and EM-024's unread twin,
both above, both under the rule at :338. The maintainer's question — whether
this is git and the method of keeping track — gets its narrow answer here:
one sentence of the method mandated a duplicate, and the duplicate did what
duplicates do. The wider answer, that half the must-fixes across the five
records are sentences and not code, is EM-024's and is already landed.

## PR Description

### Ticket
EM-025 — The per-round table has one copy, and the blocker names the row

### Tier
`standard` — a change to process documents, worked under the paragraph
beginning **A change to a process document** in "The operative test" of
`docs/tier-review-model.md`: one independent review pass, closing on that
pass, and the executor does not raise it. That pass is row 1 of the Review
table below and has not been taken.

### Summary
`docs/tier-review-model.md`, "When review ends", no longer appends the
per-round table under the `BLOCKER:` comment: the table has one copy, in the
ticket file's Review section, and a blocker, a discharge note or any summary
that needs what it holds names the row and the finding's `R<n>.<k>` instead
of restating either. The contributor policy's §3 non-convergence trigger, the
section's own index row and the pull-request template's `### Review` header
are brought with it in the same commit. No decision record is owed: this adds
a rule inside a document under an existing decision, which
`docs/adr-process.md`, **What "a workflow rule changes" reaches**, puts on the
second side, with the ticket as its record.

### Acceptance criteria
Every figure below is read from the command beside it, run at 8b0c3bd — the
last commit that changes what any of them counts — except AC4's, which is read
over the branch.
- [x] AC1: `docs/tier-review-model.md` "When review ends" no longer appends
  the table under the blocker and instead names the row —
  `grep -c 'appended to the ticket file under the' docs/tier-review-model.md`
  returns 0. The sentence now reads: "The record travels with the block: the
  per-round table has one copy, in the ticket file's Review section, and the
  `BLOCKER:` comment names the row — **One copy**, below, states the rule."
- [x] AC2: the rule carries a `Retired when:` line naming its population — the
  **One copy** paragraph is followed by one whose population is the next fifty
  closed critical-tier tickets on an adopting project, retiring the rule where
  a blocker that names a row is found by the round that reads it to have named
  the wrong row, more than once.
  `grep -c 'named the wrong row' docs/tier-review-model.md` returns 1.
- [x] AC3: `templates/PR-DESCRIPTION.md` `### Review` states that the table has
  one copy —
  `grep -c 'The table appears once, here' templates/PR-DESCRIPTION.md` returns
  1, added to the header EM-007-002 amended rather than in place of it, so that
  the header still says which tiers write the section and how many rows a
  process-document change has — and §3's blocker guidance points at the row:
  `grep -c 'the blocker names the rows and the' docs/ai-contributor-policy.md`
  returns 1.
- [x] AC4: this ticket's file carries the table header at most once at every
  commit on the branch. Reading every commit since `main` at 9924809:
  `for c in $(git rev-list 9924809..HEAD); do git show "$c:docs/tickets/active/EM-025-the-per-round-table-has-one-copy-and-the-blocker-names-the-row.md" 2>/dev/null | grep -c '^| Round | Must-fix |'; done`
  returns 0 at each commit before this description and 1 at the commit that
  adds it, and no other value.
- [x] AC5: the index and the map are consistent with the amended section in the
  same commit, 8b0c3bd. The "When review ends" row of the index in
  `docs/tier-review-model.md`, "What is in this document", now reads "The three
  conditions, the round cap, the per-round record and its one copy, and the
  read before a repair is handed back" —
  `grep -c 'the per-round record and its one copy' docs/tier-review-model.md`
  returns 1. The map in `docs/ai-contributor-policy.md`, "Which document
  settles what", is unchanged and correct under each of its three triggers: no
  governed document was added, removed or renamed; no question moved to another
  document; and the row naming `docs/tier-review-model.md` already settles what
  a review reports and when it ends, which is where this rule sits.

### Falsification
N/A — no suite. Per criterion, what a reader does differently:
- AC1 — an executor blocking at the cap writes the table into the Review
  section and a pointer under the `BLOCKER:` comment, where the sentence
  removed told them to write a second table.
- AC2 — a reviewer meeting a blocker that named the wrong row records the
  finding against this line rather than against the ticket alone, and a
  maintainer asking whether the rule has earned its place has a population to
  count.
- AC3 — an executor filling the template writes the table once and points at
  it; an executor reading §3 for what a block carries is not sent to copy the
  record into the blocker.
- AC4 — a reader grepping this ticket for the table header finds one site, so
  the ticket reads as an instance of the rule it lands.
- AC5 — a reader who reaches "When review ends" from the index is told the
  section settles where the record's one copy lives, rather than learning it
  only on reaching the end of the section.

### Out of scope (per ticket)
- The three drafts the ticket records as refuted — a ceiling on the record's
  length, citing figures from harness artefacts rather than transcribing them,
  and pinning `path:line` citations to a commit — are not attempted; nothing in
  `git diff 9924809..HEAD` touches record length, artefact citation or citation
  pinning.
- The records the ticket's Context names are not repaired: no ticket file other
  than this one is changed. `git diff --stat 9924809..HEAD -- docs/tickets`
  lists this file alone.

### How to verify
1. `git diff 9924809..8b0c3bd` — three files: the **One copy** paragraph, its
   falsifier, the amended sentence and the index row in
   `docs/tier-review-model.md`; the non-convergence clause in §3 of
   `docs/ai-contributor-policy.md`; the `### Review` header in
   `templates/PR-DESCRIPTION.md`.
2. Read whole, as they stand: "When review ends" in
   `docs/tier-review-model.md`; §3 of `docs/ai-contributor-policy.md`; and "A
   number determined elsewhere has one site that goes red" in
   `docs/quality-gates.md`, which is the rule this one applies to a table.
3. The instances the rule names. EM-024's is readable from this repository:
   `git show c6ee58b:docs/tickets/active/EM-024-a-count-in-prose-has-no-falsifier.md | sed -n '324,330p'`
   records that one copy of a phrase was fixed and its twin, in a sub-section
   the executor did not read, was not, and `git ls-remote --heads origin` shows
   that branch on `origin` at c6ee58b. OMN-022-002's is on the control-plane
   project's `main` at 412e714, line 813, and is not readable from here.

### Risks / follow-ups
- `templates/PR-DESCRIPTION.md` allows a gitignored `PR.md` at the worktree
  root as a working draft while a ticket is in flight. The rule binds copies
  **in the ticket file**, so a draft's table is outside it; an executor who
  reads the rule more widely will find it says nothing about the draft, and a
  reviewer who reads it more narrowly will not look there. Nothing here changes
  the draft's standing.
- The falsifier's population is closed `critical`-tier tickets, and under "The
  operative test" a change to a process document is `standard` on one pass. On
  a repository that ships only process documents that population accrues slowly
  or not at all, so the evidence that would retire this rule comes from
  adopting projects carrying `critical`-tier work.

### Review
Not yet taken: the one independent pass this tier requires is row 1 below.

| Round | Must-fix | Where (rules / lists / documents / tests) | Inside previous round's fix | Repaired by |
|---|---|---|---|---|
