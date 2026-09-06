---
id: EM-018
title: The templates cite files this repository does not publish
status: done
tier: standard
complexity: S
dependencies: []
claimed_by: claude-fable-5-1
claimed_at: 2026-09-06
closed_at: 2026-09-06
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

### Ticket
EM-018 — The templates cite files this repository does not publish

### Tier
standard — `trivial` by the operative test's line (documentation, no
program executes it), proposed `standard` by the author because the
templates are instructions an adopter follows; an executor may not lower
it, so it stands.

### Summary
The three templates now send a reader only to files this repository
publishes, or name `DESIGN.md` in each place as the adopting project's own.
`AGENTS.md`, `CONTRIBUTING.md` §3, §4 and §6–§7 become
`docs/ai-contributor-policy.md`, `templates/PR-DESCRIPTION.md`,
`docs/tier-review-model.md` and `docs/ticket-lifecycle.md`; `backlog/` is
described as a fifth directory an adopting project may keep; `phase` is
kept and marked optional; the worked-example pointer names
`examples/tickets/PRJ-001-repo-skeleton.md`. No section list changes. The
rule the ticket states — a published template's references resolve —
carries its falsifier in `templates/TICKET.md`, "How to use this
template", stated once and in no other template.

### Acceptance criteria
Every figure below is read from the command beside it, run at 5e42924,
the last commit that changes what it counts; the description and close
commits touch no template and add no `phase:` field.

- [x] AC1: the ticket's grep returns only references that name the
  adopting project's own documents in those words. The command as the
  ticket writes it, `grep -n "DESIGN.md\|CONTRIBUTING.md\|AGENTS.md\|backlog/"
  templates/`, returns `grep: templates/: Is a directory` and exit 2; run
  with `-r` it returns seven lines, and each carries "adopting project" on
  the line the match is on:
  ```
  templates/ADR.md:6:- **Related:** <ticket IDs, other ADR IDs, sections of the adopting project's own DESIGN.md>
  templates/ADR.md:13:the adopting project's own DESIGN.md that this ADR supplements or
  templates/ADR.md:82:- A locked decision in the adopting project's own DESIGN.md needs revision.
  templates/TICKET.md:6:phase:                 # optional; a phase of the adopting project's own DESIGN.md, if it keeps one
  templates/TICKET.md:21:the adopting project's own DESIGN.md it advances.
  templates/TICKET.md:34:an adopting project may keep a fifth directory, `backlog/`, for such
  templates/TICKET.md:79:- The adopting project's own DESIGN.md §X.Y, §X.Z
  ```
  `CONTRIBUTING.md` and `AGENTS.md` no longer appear in any template.
- [x] AC2: every repository-relative path named in a template exists.
  Command, with the placeholders it excludes stated below:
  ```
  grep -ohE '`[^`]*/[^`]*`' templates/*.md | tr -d '`' \
    | grep -v '[<*]\|XXX\|NNNN\|foo\|N/A\|core/\|tests/unit/' | sort -u \
    | while read p; do if [ -e "$p" ] || [ -e "docs/tickets/$p" ]; then echo "exists   $p"; \
      elif [ "$p" = backlog/ ]; then echo "adopter  $p"; else echo "MISSING  $p"; fi; done
  ```
  Output: fifteen lines, none `MISSING` — `active/`, `blocked/`, `done/`,
  `ready/` (bare names the status table pairs with `docs/tickets/`, tested
  there), `docs/ai-contributor-policy.md`, `docs/ticket-lifecycle.md`,
  `docs/tier-review-model.md`, the four `docs/tickets/*/` directories,
  `examples/adr/`, `examples/tickets/PRJ-001-repo-skeleton.md`,
  `templates/PR-DESCRIPTION.md` exist; `backlog/` is the adopter's own
  under AC1. Excluded as placeholders, which illustrate a form and send a
  reader nowhere: `core/foo/bar.py`, `tests/unit/test_bar.py`,
  `core/modifiers.py:42`, `tests/unit/test_modifiers.py::test_caps_sv`,
  `pytest tests/unit/test_modifiers.py`, `docs/adr/NNNN-<kebab-case-slug>.md`,
  `docs/tickets/ready/PRJ-XXX-<short-slug>.md`, `docs/ticket-PRJ-XXX`, the
  two glob commands over `PRJ-284-*` and `PRJ-XXX-*`, and `N/A`. A reviewer
  who counts any of those as a reference finds it in EM-018-001's scope
  (the branch name) or in a filled-in example section (the rest).
- [x] AC3: `phase` is consistent between the template and the tickets.
  `grep -l '^phase:' docs/tickets/*/*.md | wc -l` returns 0, over the 36
  files `ls docs/tickets/*/*.md | wc -l` counts at 5e42924; the template's
  line 6 reads `phase:                 # optional; ...` by
  `grep -n '^phase:' templates/TICKET.md`. An optional field that no ticket
  carries is consistent. The seven example tickets all carry it
  (`grep -l '^phase:' examples/tickets/*.md | wc -l` returns 7 of the 7
  `ls examples/tickets/*.md` lists), which is why it is kept rather than
  removed.
- [x] AC4: no template's structure or section list changes.
  `git show <commit>:templates/<file> | grep '^#'` over the three files
  gives 39 headings at ce59c8f and 39 at 5e42924, and `diff` over the two
  lists is empty.

### Falsification
N/A — no program executes a template. Per acceptance criterion, what an
adopter copying the template does differently:
- AC1 — follows a pointer to `docs/ai-contributor-policy.md`,
  `docs/ticket-lifecycle.md`, `docs/tier-review-model.md` or
  `templates/PR-DESCRIPTION.md` and finds the answer there, instead of
  searching this repository for a `CONTRIBUTING.md` it does not publish;
  reads `DESIGN.md` and `backlog/` as things to supply, not to find.
- AC2 — opens `examples/tickets/PRJ-001-repo-skeleton.md` for the worked
  example instead of a `docs/tickets/ready/` path that was never here.
- AC3 — copies the frontmatter and leaves `phase` blank or deletes it
  without wondering whether the ticket is malformed; a project that maps
  the field to its own phases keeps doing so.
- AC4 — an adopter who copied the templates before this change finds the
  same sections in the same order and need not re-copy.
No review findings: standard tier, no round.

### Out of scope (per ticket)
Nothing here publishes an equivalent of `DESIGN.md`, `CONTRIBUTING.md` or
`AGENTS.md`, and nothing changes what a template asks for. Four judgements
at the edge of the Behaviour, each stated so a reviewer can disagree:
- The PR Description note's parenthetical list of sub-sections went with
  the `CONTRIBUTING.md §3` reference it qualified. The note now points at
  `templates/PR-DESCRIPTION.md`, which the lifecycle's "Closing" step calls
  the one list of what the description contains; the parenthetical named
  seven sections and omitted Falsification and Review, so keeping it beside
  the corrected pointer would have sent the adopter a stale list.
- `to-engine/`, an inbox directory the source project kept, is dropped from
  the list of sources a flat ticket may come from. The ticket's Context did
  not enumerate it; its Behaviour's first bullet covers it; the list of
  sources is otherwise unchanged.
- The `ADR-0038` pointer in step 1 now says where the record is
  (`examples/adr/`) and names the lifecycle's "Lineage" section as the
  rule; the id alone resolved to nothing under `docs/adr/`.
- Step 5's branch name and `master`, step 1's id lookup from the tree, and
  the claim that `PR.md` is gitignored are what the template asks for, not
  where it points, and are left as found. They are EM-018-001, raised at
  5e42924.

The map in `docs/ai-contributor-policy.md`, "Which document settles what",
names `templates/` for the shape of a ticket, a description and a record.
This change moves no question: the templates settle the same shapes, and
the documents they now point at — the policy, the lifecycle, the tier
model — settle what they settled before. The map is unchanged and needs
no update.

### How to verify
1. `git diff ce59c8f 5e42924 -- templates/` — three files, every hunk a
   reference or the falsifier paragraph.
2. Run the AC1 grep with `-r` and read the seven lines.
3. Run the AC2 loop above; expect no `MISSING`.
4. `git show ce59c8f:templates/TICKET.md | grep '^#'` against
   `git show 5e42924:templates/TICKET.md | grep '^#'`; likewise the other
   two templates.
5. Read `templates/TICKET.md` whole; the falsifier paragraph sits at the
   end of "How to use this template".

### Risks / follow-ups
- EM-018-001 — the how-to-use steps disagree with the lifecycle on the
  branch name, the id lookup and the `PR.md` claim; raised, not fixed.
- The falsifier is stated in one template and not referenced from the
  other two. The rule is stated in full only there, which is what the tier
  model asks; an adopter copying only `templates/ADR.md` does not see it.
- An adopter who copied `phase: 1` and built tooling on a number now finds
  the template blank there. The field is kept and the comment says
  optional; nothing an adopter already wrote becomes wrong.
- Two placeholder paths in the filled-in examples (`core/foo/bar.py`,
  `tests/unit/test_bar.py`) look like references to a grep and are not;
  the falsifier paragraph says so, so that a later reader does not re-raise
  this ticket against them.

### Review
N/A — standard tier.
