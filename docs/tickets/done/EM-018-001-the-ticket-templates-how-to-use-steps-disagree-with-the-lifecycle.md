---
id: EM-018-001
title: The ticket template's how-to-use steps disagree with the lifecycle on three points
status: done
tier: standard
complexity: S
dependencies: []
claimed_by: claude-fable-5-1
claimed_at: 2026-09-06
closed_at: 2026-09-06
---

# EM-018-001 — The ticket template's how-to-use steps disagree with the lifecycle on three points

## Context

Raised while working EM-018, from reading `templates/TICKET.md` whole after
its references were repointed at 2480575. EM-018 made the template's
references resolve; it left what the template's "How to use this template"
steps say to do, which was out of its scope. Three of those instructions
contradict `docs/ticket-lifecycle.md`, the document the template now sends
its reader to for the procedure:

- Step 5 says to commit on a `docs/ticket-PRJ-XXX` branch, or directly to
  `master`. The lifecycle's "Claiming" step 1 and the contributor policy's
  §7 checklist require a branch whose name begins with the ticket
  identifier, and this repository's default branch is `main`.
- Step 1 finds the next lineage id with `ls docs/tickets/*/PRJ-284-*` and the
  next flat id as the highest across the four directories. The lifecycle's
  "Lineage" section says the next id comes from history, not the tree, with
  `git log --diff-filter=A --name-only --format= -- docs/tickets`, and
  records the reused id that taught it.
- The PR Description note says a `PR.md` draft at the worktree root "is
  gitignored", and `templates/PR-DESCRIPTION.md` says the same. The
  `.gitignore` at ce59c8f lists five patterns and `PR.md` is not one of
  them, so an adopter who takes the sentence at its word commits the draft.

An adopter reading the template and the lifecycle side by side is given two
procedures and told to follow both; the one enforced by nothing is the one
dropped, as the lifecycle says of conventions that cannot both be followed.

## Specification

Documentation changes only. The template's instructions agree with the
lifecycle; the template's structure does not change.

### Files

- `templates/TICKET.md`
- `templates/PR-DESCRIPTION.md` — the `PR.md` sentence only
- `.gitignore` — only if the `PR.md` claim is kept rather than reworded

### Public surface

The templates are the surface an adopter copies; their instructions are
what an adopter does.

### Behaviour

- Step 5 names a branch whose name begins with the ticket identifier and
  does not name `master`.
- Step 1's id lookup matches the lifecycle's "Lineage" section, or points
  at it instead of restating it.
- The `PR.md` sentence is true of this repository: either `.gitignore`
  ignores `PR.md`, or the sentence says the adopting project ignores it.
- No rule is added; this ticket carries no falsifier of its own.

## Acceptance criteria

1. AC1: `grep -n "master\|docs/ticket-PRJ" templates/TICKET.md` returns
   nothing.
2. AC2: The id lookup in `templates/TICKET.md` and the one in
   `docs/ticket-lifecycle.md`, "Lineage", give the same next id on this
   repository's history.
3. AC3: `PR.md` is either matched by `.gitignore` or not claimed to be.
4. AC4: No template's structure or section list changes.

## Out of scope

- Any further reference repointing; EM-018 did that.
- Changing what the lifecycle says; the template follows the lifecycle,
  not the other way round.

## References

- `docs/ticket-lifecycle.md`, "Claiming" and "Lineage".
- `docs/ai-contributor-policy.md`, §7.
- EM-018 — the ticket this was found under.

## Notes

Proposed `standard` for the reason EM-018 gives: the change alters
instructions an adopter follows, and EM-007-002 owns the disagreement
between that reading and the operative test's `trivial` line.

## PR Description

### Ticket
EM-018-001 — The ticket template's how-to-use steps disagree with the
lifecycle on three points

### Tier
standard — proposed by the author for the reason EM-018 gives, and the
change now also adds a line to `.gitignore`, a data file a program (git)
loads, which the operative test's line places at least at `standard` on
its own account. No clause of the test holds: no caller, contract,
ordering, seed or process surface is touched.

### Summary
`templates/TICKET.md`, "How to use this template", now says what
`docs/ticket-lifecycle.md` says: step 5 asks for a branch whose name
begins with the ticket identifier and names no default branch; step 1
finds the next lineage id from the set of ticket files ever added, with
the command the lifecycle's "Lineage" gives, and continues the flat
sequence from that same history rather than from the four directories.
`/PR.md` is added to `.gitignore`, so the sentence in both templates
saying a root `PR.md` draft is gitignored is true of this repository
without being reworded. No template's section list changes.

### Acceptance criteria
Every figure below is read from the command beside it, run at 5750d73,
the last commit that changes what it counts; the description and close
commits touch no template and not `.gitignore`.

- [x] AC1: `grep -n "master\|docs/ticket-PRJ" templates/TICKET.md`
  returns nothing; exit status 1.
- [x] AC2: the template and the lifecycle now name one command, so the
  two lookups agree by construction; run at 5750d73 they agree in fact.
  `git log --diff-filter=A --name-only --format= -- docs/tickets | grep -oE
  "EM-[0-9]{3}(-[0-9]{3})*" | sort -u` is the lifecycle's command with the
  ids extracted from the paths; filtered to children of EM-018 it returns
  `EM-018-001`, so the next child is EM-018-002, and filtered to flat ids
  its highest is `EM-021`, so the next flat id is EM-022. The lookup the
  template gave before this change disagrees with it where the lifecycle
  says it does: `ls docs/tickets/*/ | grep -oE "EM-010-[0-9]{3}"` returns
  `EM-010-002` alone, while the history command filtered the same way
  returns `EM-010-001` and `EM-010-002`.
- [x] AC3: `git check-ignore -v PR.md` returns `.gitignore:6:/PR.md
  PR.md`; `grep -c . .gitignore` returns 6 lines at 5750d73 against the 5
  the ticket counts at ce59c8f. The sentence in
  `templates/PR-DESCRIPTION.md` and the note in `templates/TICKET.md`,
  "PR Description", are unchanged and now true.
- [x] AC4: `diff <(git show e6cc59c:templates/<file> | grep '^#') <(git
  show 5750d73:templates/<file> | grep '^#')` is empty, exit 0, for each
  of the three templates: 15, 12 and 12 headings at e6cc59c and the same
  at 5750d73 for `TICKET.md`, `PR-DESCRIPTION.md` and `ADR.md`.
  `git diff --stat e6cc59c 5750d73 -- templates .gitignore` names two
  files, `templates/TICKET.md` and `.gitignore`.

### Falsification
N/A — no program executes a template, and the `.gitignore` line adds a
pattern git reads without changing anything a test could pin. Per
acceptance criterion, what an adopter copying the template does
differently:
- AC1 — branches with the ticket identifier at the head of the name, as
  the contributor policy's §7 will ask at pre-flight, instead of on a
  `docs/ticket-` branch that fails that tick, and does not look for a
  `master` this repository does not have.
- AC2 — reads the next id from history and does not hand out an id a
  deleted or renamed ticket spent; on this repository, an adopter following
  the old step would offer EM-010-001 again.
- AC3 — keeps a `PR.md` draft at the root while a ticket is in flight and
  finds `git status` silent about it, instead of committing it on the
  template's word; `git check-ignore` is the check.
- AC4 — an adopter who copied the templates before this change finds the
  same sections in the same order and need not re-copy.
No review findings: standard tier, no round.

### Out of scope (per ticket)
Nothing here changes what the lifecycle says, and no reference is
repointed beyond the two section names step 5 and step 1 now cite. Four
judgements at the edge of the Behaviour, each stated so a reviewer can
disagree:
- `.gitignore` rather than rewording. The draft is a real convenience the
  templates already permit, and a true sentence with the pattern behind
  it costs one line; a reworded sentence would have left the convenience
  in place with nothing making it safe. The pattern is `/PR.md`, anchored
  to the root, because the templates permit the draft at the root only;
  an unanchored `PR.md` would also hide a draft left in a subdirectory,
  which nothing permits.
- The `PR.md` sentence in `templates/PR-DESCRIPTION.md` is not edited. The
  ticket lists it as a file to change only if the claim is reworded; the
  claim is kept and made true instead. An adopter copying the templates to
  a project without the pattern reads a sentence that is true here and
  becomes true there by copying the line; that gap is the ticket's stated
  alternative, not a finding against it.
- Step 1 restates the lifecycle's command rather than only pointing at it.
  The ticket allows either. An adopter copies `templates/` and needs a
  runnable instruction; the command is the lifecycle's own, word for word,
  and AC2 is the check that the two stay the same. The reason — a spent id
  — is given in one clause and the rest is left to "Lineage".
- Step 5 says which branch for a ticket raised while working another: the
  originating ticket's, which is where "Lineage" creates one raised by a
  review. The step before named one branch for every case; a step that
  named only "a branch beginning with the ticket identifier" would have
  sent the executor of a child ticket off its parent's branch, against the
  lifecycle.

The map in `docs/ai-contributor-policy.md`, "Which document settles what",
names `templates/` for the shape of a ticket and `docs/ticket-lifecycle.md`
for the lineage rule; this change moves no question between them, and the
map is unchanged.

### How to verify
1. `git diff e6cc59c 5750d73 -- templates .gitignore` — two files, three
   hunks: step 1's two bullets, step 5, and one `.gitignore` line.
2. Run the AC1 grep; expect no output and exit 1.
3. Run the AC2 history command and compare its EM-010 children with `ls
   docs/tickets/*/`; expect the history to show one more.
4. `git check-ignore -v PR.md`; expect `.gitignore:6:/PR.md`.
5. Run the AC4 diff for each of the three templates; expect empty.
6. Read `templates/TICKET.md`, "How to use this template", whole beside
   `docs/ticket-lifecycle.md`, "Claiming" and "Lineage".

### Risks / follow-ups
- The command now lives in two documents that must agree. AC2 is the
  check, and the lifecycle's "Lineage" is where a change to it is made
  first; the template follows.
- Step 1 says "ids extracted from the paths" and gives no extraction
  command, as the lifecycle does not; an adopter's ticket prefix is theirs
  to grep for.
- No child ticket raised.

### Review
N/A — standard tier.
