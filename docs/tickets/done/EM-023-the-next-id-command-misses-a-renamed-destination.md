---
id: EM-023
title: The next-id command misses an id created by renaming a ticket file
status: done
tier: standard
complexity: S
dependencies: []
claimed_by: claude-opus-5
claimed_at: 2026-09-15
closed_at: 2026-09-15
---

# EM-023 — The next-id command misses a renamed destination

## Context

`docs/ticket-lifecycle.md`, "Lineage", says an id once created is spent, and
prescribes how to find the next one:

> Take the next number from the set of ticket files ever added — `git log
> --diff-filter=A --name-only --format= -- docs/tickets`, with the ids
> extracted from the paths — not from `ls`.

`--diff-filter=A` selects additions. An id created by **renaming** an existing
ticket file is recorded as a rename, not an addition, so its new id never
appears in that command's output. The rule protects against reusing an id
whose file was later removed; it does not protect against reusing an id that
arrived as a rename destination.

Measured on the control-plane project on 2026-09-08. `OMN-029` exists in
`docs/tickets/done/` on that repository's default branch, and was created by
renaming `OMN-028` after two agents allocated that identifier concurrently.
Against its history:

- `git log --all --diff-filter=A --name-only --format= -- docs/tickets/ | grep -oE "OMN-[0-9]{3}" | sort -u | tail -1` returns **OMN-028**.
- The same command with `--diff-filter=AR` returns **OMN-029**.
- Every id in the tree of every ref returns **OMN-029**.

So a contributor following the documented instruction on that repository would
have taken `OMN-029` as the next free identifier, and allocated an id already
in use — the exact failure the paragraph exists to prevent, reached by the one
route it does not cover.

This repository is not currently exposed: `EM-014-001` was created as an
addition rather than a rename, so the command sees it, and no EM id has
arrived by rename. The defect is in the published instruction, not in this
repository's history, and it reaches any project that adopts the rule and ever
renames a ticket file — which the same paragraph explicitly contemplates when
it says an id "raised and later deleted, absorbed or **renamed** leaves no
file".

## Specification

Documentation change only. The rule is unchanged; the command it prescribes is
corrected so that it answers the question the rule asks.

### Files

- `docs/ticket-lifecycle.md` — the "Lineage" paragraph's command
- `templates/TICKET.md` — its "How to use this template" step 1, if it repeats
  the command

### Public surface

The command is an instruction an adopter follows. Its output decides which
identifier they allocate, so a command that under-reports spent ids produces
collisions in the adopting project rather than in this one.

### Behaviour

- The prescribed command reports every id ever borne by a ticket file,
  including one that arrived as a rename destination. `--diff-filter=AR` is
  the minimal correction; a reader of every ref's tree is stronger and slower.
  Whichever is chosen, the paragraph says what it covers and what it does not.
- The paragraph states the case it now covers, so the next reader can see why
  the flag is what it is — the same way it already records the spent-id case
  that produced the original rule.
- The worked figures name the command that produced them and the repository
  and date they were taken at, per the contributor policy's §6.
- **This ticket adds no rule**, so it states no falsifier of its own; the
  existing rule's falsifier is unchanged.

## Acceptance criteria

1. AC1: the command in `docs/ticket-lifecycle.md`, run against a history in
   which a ticket file has been renamed to a new id, reports that id.
2. AC2: `templates/TICKET.md` and the lifecycle give the same command.
3. AC3: the paragraph states which allocation routes the command covers, and
   names the rename case as one of them.
4. AC4: no rule changes; the diff adds no `Retired when:` line and removes
   none.

## Out of scope

- The concurrent-allocation failure that produced `OMN-029` in the first
  place: two agents on refs neither could see, which no command over one
  repository's history can catch. That is a different defect with a different
  answer, and it belongs to whichever project meets it a second time.
- Renumbering any existing ticket.

## References

- `docs/ticket-lifecycle.md`, "Lineage" — the rule and the command
- `templates/TICKET.md`, "How to use this template" — where the command is
  repeated for an adopter
- The control-plane project's `OMN-029`, and the collision record in its own
  Notes, which is the measurement above

## Notes

Proposed `standard`: the change alters an instruction an adopter follows, and
under the operative test as it stands a process document that states no rule a
program executes is otherwise `trivial`. The tier question EM-007-002 owns
applies here as it does to every documentation ticket on this board; the
executor may raise and never lower, so the higher tier is the one an author
can propose without resolving it.

## PR Description

### Ticket
EM-023 — The next-id command misses an id created by renaming a ticket file.

### Tier
`standard`, on one independent review pass. The change alters instructions in
`docs/ticket-lifecycle.md`, `templates/TICKET.md` and a decision record under
`examples/adr/`, all of which state procedures a contributor performs, so "The
operative test" fixes the tier there. The ticket's Notes proposed `standard`
before ADR-0004 settled the question; the answer is the same. The pass ran
against d863e73 and is row 1 of the Review table.

### Summary
`--diff-filter=A` selects additions, so an id that arrives by renaming a
ticket file never appears and a contributor following the documented
instruction allocates an id already in use. The review then found that the
same command drops a merged side branch whose net effect on `docs/tickets` is
nil, losing the deleted-and-absorbed case the rule was written for. The
command now reads `git log --full-history --diff-filter=AR --name-only
--format= -- docs/tickets` at every site that states it, and the paragraph
says what each flag answers and what the command does not reach.

### Acceptance criteria
- [x] AC1: the command, run against a history in which a ticket file has been
  renamed to a new id, reports that id. Built as a throwaway history: commit
  `docs/tickets/ready/PRJ-028-first.md`, `git mv` it to
  `docs/tickets/ready/PRJ-029-first.md`, commit. The old form
  (`--diff-filter=A`) returns `PRJ-028`; the prescribed form returns `PRJ-028`
  and `PRJ-029`. Both were run against that history, not against this
  repository, because this repository has no rename-created id — which is
  what the ticket's own Context says and what AC1's evidence therefore has to
  be constructed to show.
- [x] AC2: `templates/TICKET.md` and `docs/ticket-lifecycle.md` give the same
  command. `grep -rn "diff-filter" docs/ticket-lifecycle.md templates/TICKET.md
  examples/adr/*.md`, run after c6943db, returns the same flags and path at
  every site, wrapping aside — and a third site the ticket's Files did not
  name; see the departure recorded below.
- [x] AC3: the paragraph states which allocation routes the command covers and
  names the rename case as one of them. It carries a bullet per flag, each
  with the route it answers and the history that refutes the recipe without
  it, then a closing paragraph on what the command covers, what `--all` adds,
  and what no form reaches.
- [x] AC4: no rule changes. `git diff main...HEAD | grep -E '^[+-].*Retired
  when'`, run after c6943db, returns nothing: no falsifier is added, removed
  or altered, and the rule the paragraph states is the same rule.

### Falsification
N/A for a behavioural claim — this repository publishes documents and runs no
suite. Per criterion, what a reader does differently: a contributor allocating
an id runs a command that reports ids spent by rename and ids spent on an
absorbed branch, and stops handing out an id already in use.

For each review finding repaired, per the contributor policy's §6:

- R1.1 — class: **which claims does the recipe make that running it would
  refute?** The coverage sentence is the instance. The question was asked of
  every claim the paragraph makes about its own command, each tested against a
  history built to break it. Siblings:
  - **"every id borne by a file under `docs/tickets` on the refs the command
    is run against"** — the instance, and false. Built: raise
    `PRJ-040-raised.md` on a branch, `git rm` it on that branch, merge the
    branch, delete it. The command as written returns `PRJ-001` alone;
    `--full-history` returns `PRJ-001` and `PRJ-040`. Repaired by adding the
    flag and restating the coverage.
  - **"a rename ... never appears under `A`"** — checked and true, but only
    with rename detection on, which the command has by default. The qualifier
    is now in the text. A renumber below git's similarity threshold is
    recorded as a delete plus an addition and caught by `A` anyway.
  - **"no command over one repository's history catches it"** — checked and
    overbroad. The command reads the ref it is run on; `--all` reads every ref
    the repository holds. Repaired: the sentence now separates what `--all`
    adds from what nothing reaches.
  What a reader does differently: a reader who runs the recipe on a history
  with an absorbed branch gets the id that history spent, instead of a promise
  that it would have been reported.
- R1.2 — class: **which sites state the next-id command?** The lifecycle
  paragraph and the template's step 1 are the two the ticket's Files names.
  The question was asked of the tree by `grep -rln "diff-filter" --include=*.md
  . `, run after c6943db. Siblings:
  - **`docs/ticket-lifecycle.md`, "Lineage"** — the rule's own statement.
    Corrected.
  - **`templates/TICKET.md`, step 1** — corrected.
  - **`examples/adr/adr-0038-...md`** — the only runnable, copy-pasteable form
    in the repository, and the record the template's step 1 sends a first-time
    adopter to by name. It still read `--diff-filter=A`. Corrected; see the
    departure below.
  What a reader does differently: an adopter who copies the command from the
  record the template points them at copies one that answers the question,
  rather than the one this ticket exists to fix.
- R1.3 — class: **which sentences did the insertion move, such that what they
  point back to changed?** The `EM-010-001` example is the instance. The
  question was asked of every sentence between the command and the
  Retired-when line. Siblings:
  - **"This repository already has one such id"** — the instance. It had come
    to sit after the unreachable-ref case and read as an instance of it, and
    under the new precise meaning of rename it was refuted: `git show
    --name-status 0947dda` reports a delete of `EM-010-001` and an addition of
    `EM-014-001`, not a rename. Repaired by returning it to the opening
    paragraph, saying "superseded by" rather than "renamed", and carrying it
    into the `AR` bullet as the reason this repository was not exposed.
  - **The fourteen-ids sentence and the reused-id sentence** — checked; both
    still attach to the opening paragraph's subject and were not moved.
  What a reader does differently: a reader of the example is not told that a
  delete-plus-addition is a rename, three lines after being told precisely
  what a rename is.
- R1.4, R1.5, R1.6 — notes. Repaired in the round; a note carries nothing
  under §6 as EM-009-001 narrowed it.

### Departure from Files, recorded
The ticket's Files names `docs/ticket-lifecycle.md` and `templates/TICKET.md`.
This change also edits
`examples/adr/adr-0038-tickets-carry-the-lineage-of-the-ticket-that-raised-them.md`,
one line, the `--diff-filter` in its script block.

The reason is §6's class obligation, which EM-009-001 narrowed to must-fixes
and which this is one of: the class is every site stating the command, and
repairing two of three is repairing the instance while leaving a sibling that
the template actively routes adopters to. Leaving it would have shipped a
known-wrong runnable copy of the exact command the ticket exists to correct.

Whether a review-named remedy may be taken in the round like this, rather than
blocked under the contributor policy's §3, is the open question EM-020-001
owns and the maintainer holds; this is recorded here so it is one more
instance for whichever way that goes, and so the maintainer reads it at close.
No decision the ticket makes is changed by it.

### Out of scope (per ticket)
Confirmed.
- The concurrent-allocation failure that produced `OMN-029` — described and
  explicitly left; the closing paragraph says no form of the command reaches
  an id on a ref the repository has never seen.
- Renumbering any existing ticket — nothing is renumbered. The clause that
  offered renumbering as a reason a file is renamed is dropped, because it sat
  eleven lines above the rule refusing exactly that.

### How to verify
1. `sed -n '/^\*\*The next id comes from history/,/^\*\*Retired when:\*\* the project forbids/p' docs/ticket-lifecycle.md`
   — the rule, the command, a bullet per flag, and the coverage paragraph.
2. `grep -rn "diff-filter" --include=*.md docs templates examples` — three
   sites, all `--full-history --diff-filter=AR`, and no fourth.
3. Rebuild AC1's history: `git init`, commit `docs/tickets/ready/PRJ-028-first.md`,
   `git mv` to `PRJ-029-first.md`, commit; then run the command with `A` and
   with `AR` and compare.
4. Rebuild R1.1's history: raise `PRJ-040` on a branch, `git rm` it there,
   merge the branch and delete it; then run the command with and without
   `--full-history`.
5. `git diff main...HEAD | grep -E '^[+-].*Retired when'` — empty, which is
   AC4.

### Risks / follow-ups
- **Recorded, not repaired.** A ticket file *copied* to a new id is reported
  `A` by the prescribed command and by `diff.renames=copies`, but is reported
  `C` under `-C --find-copies-harder`, and `AR` then loses the id. The
  prescribed command never passes `-C`, so nothing is live; the exposure is an
  adopter who adds copy detection to the recipe. It is one instance, and "A
  rule needs a second instance" bars writing it into the documents on one, so
  it is recorded here rather than raised.
- Both the prescribed form and the old one return 50 ids on this repository,
  from the two commands quoted in AC2 and R1.1, run after c6943db. The
  difference between them is not observable here, which is why both defects
  are demonstrated on constructed histories and why this repository's own
  `EM-014-001` is described as the case that does *not* exercise the rename
  route.

### Review
One independent review pass, per "The operative test" for a change to a
process document. No second pass is taken.

| Round | Must-fix | Where (rules / lists / documents / tests) | Inside previous round's fix | Repaired by |
|---|---|---|---|---|
| 1 | 3 (of 6 findings) | documents: the coverage sentence claims every id borne on the refs read, while default history simplification drops a merged branch TREESAME on docs/tickets and loses an absorbed id entirely (must-fix); examples/adr/adr-0038 carries the only runnable form of the command and still reads `--diff-filter=A`, and the template routes adopters to it by name (must-fix); the insertion left the EM-010-001 example attached to the unreachable-ref case, where it reads as a rename instance that git records as a delete plus an addition (must-fix); the command carries no `--all` while the ticket's own evidence was taken with it; the renumber clause conflicts with the rule against renumbering a reused id eleven lines below; the two-route claim holds only while copy detection is off | — | c6943db |

Derived from the row and not asserted beside it: three must-fixes over one
review round. Round 1 has no round before it, so its inside-previous-fix cell
reads `—` and no line is uncountable.

- R1.1 · permits · must-fix · `docs/ticket-lifecycle.md`, "What this covers and what it does not" · default history simplification prunes a merged side branch that is TREESAME on `docs/tickets`, so an id created and absorbed on a branch is reported by nothing, which is the deleted-and-absorbed case the rule's own first sentence names — remedy: add `--full-history` at both sites and narrow the coverage sentence to what the command reads; cost, if the remedy tightens a control: none on this repository, where both forms return 50 ids after c6943db; on an adopting project an id abandoned on a merged branch is counted spent, which the rule's first sentence already asserts; inside previous fix: —
- R1.2 · permits · must-fix · `examples/adr/adr-0038-...md`, the script block · the only copy-pasteable form of the command still reads `--diff-filter=A`, and `templates/TICKET.md` step 1 names that record as the decision record for the rule, so the reader most likely to copy a command copies the defective one — remedy: correct the `--diff-filter` in the snippet; cost, if the remedy tightens a control: none, it corrects a stale copy and adds no refusal; inside previous fix: —
- R1.3 · permits · must-fix · `docs/ticket-lifecycle.md`, "This repository already has one such id" · the inserted paragraphs moved this sentence's antecedent, so it reads as an instance of the unreachable-ref case, and under the new precise meaning of rename it is refuted — `git show --name-status 0947dda` reports a delete and an addition — leaving the document contradicting its own ticket's Context within one paragraph — remedy: move the example back to the opening paragraph and describe what git recorded; cost, if the remedy tightens a control: none, a reordering and a correction; inside previous fix: —
- R1.4 · permits · note · `docs/ticket-lifecycle.md`, "no command over one repository's history catches it" · the prescribed command carries no `--all` and reads HEAD alone, while the ticket's own measurement used `--all`, so the claim is overbroad once another ref has been fetched — remedy: name what `--all` adds; cost: none; inside previous fix: —
- R1.5 · permits · note · `docs/ticket-lifecycle.md`, "because the ticket was renumbered" · offered as an ordinary reason a file is renamed, eleven lines above the rule that a reused id is not renumbered afterwards — remedy: drop the clause and keep the concurrent-allocation case the evidence supports; cost: none; inside previous fix: —
- R1.6 · permits · unranked · `docs/ticket-lifecycle.md`, "an id arrives by two routes" · true only while copy detection is off; under `-C --find-copies-harder` a copied file reports `C` and `AR` loses the id — remedy: qualify by the command's own rename detection; cost: none; inside previous fix: —

The reviewer found nothing in the second column and recorded that as an answer
rather than leaving the column empty: `AR`'s output is a superset of `A`'s, so
no id the old command reported is lost; the added prose imposes no obligation
and refuses no allocation; and every extra line the new flags produce carries
an id the rule's own first sentence already declares spent, which is the rule
working rather than over-tightening.

### Definition of Done (all tiers)
The four machine checks do not apply to a repository that publishes documents
and runs no suite; the falsification gate is discharged above, with N/A for
the behavioural claim and a class line per must-fix repaired. Every measured
figure names its baseline in the same sentence and is read from the command
named beside it. The independent pass a process-document change takes has run
and is recorded.
