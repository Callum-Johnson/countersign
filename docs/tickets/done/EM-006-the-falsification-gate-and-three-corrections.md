---
id: EM-006
title: Add a falsification gate, and correct three published patterns that do not compose
status: done
tier: critical
complexity: L
dependencies: [EM-002]
claimed_by: claude-fable-5-1
claimed_at: 2026-09-06
closed_at: 2026-09-06
---

# EM-006 — the falsification gate, and three corrections

## Context

A ten-ticket wave on the rules-engine project produced evidence that bears
directly on documents this repository publishes. Two findings are additions to
the model; three are defects in patterns already published here, which readers
may be copying.

The load-bearing one is a hole in `docs/quality-gates.md`. That document argues
for measuring coverage as *no regression on files you changed*, on the grounds
that this "asks the only question that matters: did *this change* come with its
tests?" The wave falsified that. Four separate changes passed the coverage rule
— one of them on a file at 100% of both statements and branches — while
shipping tests that **could not fail**. Reverting the exact line each change had
fixed left the whole suite green.

Coverage measures whether a line was *executed*. It does not measure whether an
assertion *discriminates*. A test that exercises a changed line and would pass
under the old implementation as well as the new one satisfies every gate in the
document and pins nothing.

The mechanism was the same each time, and it is not exotic. A predicate ended in
an inclusive comparison, so two candidate implementations agreed at both values
the tests used and differed only in a band between them; the tests sat outside
that band. In another instance two candidate readings of a specification
coincided on *every* fixture in the repository, which made them the same
function as far as the suite could tell — so no single test case could have
separated them, however carefully written.

None of this was caught by gates. All of it was caught by second-agent review,
and only because a reviewer mutated the code and counted. Across the wave,
**every critical-tier ticket returned findings at first review — six of six** —
and the recurring finding was not broken code. It was a true-sounding claim
*about* code that did not survive measurement. That is a strong result for the
countersignature thesis and a weak one for the gates, and both belong in the
documents.

The six-of-six figure is what the wave itself supports and is the only tally
this ticket asserts. A larger running count was in circulation while the wave
was worked and was carried between briefs without ever being derived from the
repository; it did not survive checking, and the correction is recorded here
rather than quietly dropped, because it is an instance of the same defect the
ticket is about. Anyone wanting a longer-run figure must derive it from the
closed tickets rather than inherit it. See Notes.

The three corrections concern patterns already published:

1. **ADR-0038's id namespace has two independent defects**, both of which are
   the same shape: the scheme's lookup instruction is narrower than the
   namespace it protects.

   **1a — the same id under two slugs merges silently.** The same lineage id written
   under two different slugs — one in the main working tree, one on a branch —
   produces two files for one id and **merges with no conflict**, because the
   paths differ and git compares paths. Nothing in the scheme detects it: it
   breaks the ADR's own sibling-lookup mechanic and lets two agents claim the
   same ticket from different files. The mechanism is structural and can be
   reproduced on demand; the implementer should state it that way rather than
   as an incident, because the source project's own record of how it was first
   noticed is a working-session artefact and not reconstructible from the
   repository.

   **1b — an id, once created, is spent, and the tree does not know it.** The
   ADR tells the reader to take the next flat id from the highest across the
   ticket directories. That read is of the *working tree*, and a ticket raised
   and later deleted, absorbed or renamed leaves no file behind while remaining
   named in closed tickets, commit messages and pull-request bodies. On the
   source project, measured against its default branch, **fourteen ids have
   been created and later had their file removed** — and the next flat id was
   taken, worked and closed before anyone noticed it had been used before, which
   is the fourteenth. (Measured on the branch that discovered it the figure is
   thirteen, because there the reused id has a file again; the implementer
   should quote whichever population it names, and name it.) The
   next id must come from **history** — `git log --diff-filter=A` over the
   ticket directories — not from the tree; and a reused id is not renumbered
   after the fact, consistent with the ADR's own no-retroactive-renumbering
   rule.

   ADR-0038 is published in `examples/`.

2. **A 72-character commit-subject limit does not compose with lineage ids.** A
   fourth-generation id consumes roughly a third of the line before the verb.
   On the source project the limit is now breached routinely, including by merge
   commits on the default branch. Two published conventions that cannot both be
   followed is worse than either alone. This repository publishes the lineage
   scheme and no subject-length rule, so the correction here is to state the
   hazard beside the scheme, for readers who bring a subject limit with them.

3. **The identical-script rule has a fleet failure mode.** `quality-gates.md`
   requires the local command and the CI job to be the same script, which is
   right. But on the source project that script's first step installs the
   package in editable mode, which mutates state **global to the machine**
   rather than local to the working tree. With several agents working in
   parallel worktrees, one agent running the gate script repoints every other
   agent's imports at its own tree. Three agents independently deduced this and
   refused to run the script; the gates were only trustworthy because each
   pinned its interpreter path by hand and printed it as evidence. The rule as
   written is silent on this, and a fleet is the environment this repository is
   about.

## Specification

Documentation changes only. No templates are removed; no existing rule is
deleted without a stated replacement.

### Files

- `docs/quality-gates.md` — add the falsification gate as a distinct gate
  alongside the four machine gates, and state plainly what coverage does and
  does not measure. Add the fleet caveat to the identical-script rule.
- `docs/ai-contributor-policy.md` — add the executor obligation: name the
  counterfactual, run the mutant, record the count. This is a pre-report duty,
  not something review is expected to catch.
- `templates/PR-DESCRIPTION.md` — require that every measured number name the
  baseline it was measured against, in the same sentence.
- `examples/adr/adr-0038-*.md` — annotate in place with the collision and the
  placement rule. Do not supersede it; the decision is sound and only its
  operating instructions are incomplete.
- `docs/ticket-lifecycle.md` — the placement rule in its operational form: a
  ticket raised by a review is created on the branch under review.
- `docs/ticket-lifecycle.md`, "Lineage" — state that a fixed commit-subject
  length does not compose with lineage ids, with the fourth-generation figure
  from Context, so that a reader adopting the scheme alongside such a limit
  knows to choose.
- `case-studies/` — the review-yield figure, if the implementer judges it
  belongs there rather than in a policy document. See Notes.

### Public surface

N/A — this repository publishes documents, not code. The equivalent surface is
the set of rules a reader may already have adopted; the three corrections above
change that surface and are the reason for the tier.

### Behaviour

- The falsification gate is stated as an **executor** obligation discharged
  before reporting, not as a reviewer checklist item. The distinction is the
  point: every instance in the source wave was caught by review, which means
  each one cost a full review round of rework.
- The gate's discharge is a recorded number — the count of tests that go red
  under the named wrong implementation. A count of zero means the test is
  decorative and the claim is unpinned.
- The gate states what to do when the obvious arrangement does not
  discriminate: keep the test, and **label it in its own docstring as
  non-discriminating**. An unlabelled passing test beside a real pin is how
  these claims shipped unpinned in the first place, and deleting it loses a
  regression check that is still worth having.
- The gate states the multi-rival case: when two candidate readings coincide on
  every existing fixture they are indistinguishable to the suite, so **one case
  cannot separate three readings** — a case is needed per rival.
- The identical-script rule gains the constraint that the script must not mutate
  state outside the working tree, with the editable-install example.
- The ADR-0038 annotation states the placement rule and the reason: paths
  differing means git cannot see the collision.

## What this refuses, and what it costs

> Added 2026-09-05 on review of the wave, applying EM-010's two questions to the ticket that proposes them. A figure measured here names its baseline in the same sentence; a figure from a private project names the ticket section it is taken from; an assumption says so. Raised alongside EM-014; corrected after independent review of c0111ae.

**Refuses.**

- Any behavioural change whose executor cannot construct a plausible wrong
  implementation. A refactor, a rename, a change with no discriminating band
  must either invent a mutant to satisfy the gate or label its test
  non-discriminating. The label is permitted and is the honest path, but it is
  now a declaration the executor writes and a reviewer may challenge, on every
  such change.
- Any gate script that installs the package in editable mode, which is the
  ordinary Python arrangement. A project adopting the no-global-mutation
  constraint restructures its gate or, as three agents on the source project
  did, refuses to run it as written.
- Nothing, on the subject-length point. No subject-length rule appears in
  `docs/` or `templates/` at 8b0a8b4, so there is none to replace; AC7 states
  the composition hazard beside the lineage scheme and refuses no convention.
  A reader who brought a 72-character limit from elsewhere is told the two do
  not compose and left to choose.

**Costs.**

- Per behavioural claim: construct the mutant, run the suite, record the
  count. That is at least one additional full suite run per claim. On the
  twelve-minute gate run EM-012 reports from OMN-025's pull-request
  description, a change carrying three claims pays roughly thirty-six minutes
  of gate time before reporting, against a baseline of one run. Claims per
  ticket and suite runs per ticket are a question for an adopting project on
  its first five critical tickets under the gate; this repository has no
  suite and cannot measure them.
- Baseline-in-sentence is a writing cost only, but it applies to every number
  in every pull-request description from now on.
- Reviewer brief: five of the documents this wave edits total 3,150 words,
  measured 2026-09-05 at commit 8b0a8b4 (tier-review-model 761, quality-gates
  411, ai-contributor-policy 1,034, ticket-lifecycle 544, PR-DESCRIPTION 400).
  This ticket adds to four of them and removes from none; its corrections are
  an in-place annotation of ADR-0038 and a stated hazard beside the lineage
  scheme. AC10 makes the re-measurement at close an acceptance criterion
  rather than a wish, at the cost of one word count per edited file.

## Acceptance criteria

1. AC1: `docs/quality-gates.md` states, in its own section, that coverage
   measures execution and not discrimination, and gives the mechanism by which a
   fully-covered file can be fully unpinned.
2. AC2: The falsification gate is specified as an executor obligation with a
   recorded red count, and the document says what a count of zero means.
3. AC3: The non-discriminating-case rule and the one-case-per-rival rule are
   both stated.
4. AC4: `docs/ai-contributor-policy.md` and `templates/PR-DESCRIPTION.md`
   between them require that a measured number names its baseline in the same
   sentence, without duplicating the rule in full in both places.
5. AC5: The identical-script rule states the no-global-mutation constraint and
   gives the editable-install failure as its example.
6. AC6: `examples/adr/adr-0038-*.md` carries an in-place annotation covering
   **both** namespace defects — the silent slug collision with its
   on-the-branch placement rule, and the spent-id problem with its
   next-id-from-history rule — and `docs/ticket-lifecycle.md` carries both in
   operational form. The ADR is not superseded.
7. AC7: `docs/ticket-lifecycle.md` states beside the lineage scheme that a
   fixed commit-subject length does not compose with lineage ids, and why. No
   subject-length rule is introduced, replaced or removed, since none is
   published here.
8. AC8: No third-party material enters the repository. The source project
   implements a third party's ruleset; every example is stated in engineering
   terms — inclusive comparisons, discriminating bands, fixture coincidence —
   with no domain content. `DISCLOSURE.md` needs no amendment as a result of
   this ticket, or it is amended and says why.
9. AC9: Critical tier per ADR-0002: an independent agent that did not perform
   the work reviews this against the artifacts, and its findings are recorded in
   the pull-request description.
10. AC10: The pull-request description states the word count of every file
    this ticket edits, before and after — the four documents figured in the
    section above against those figures, and `examples/adr/adr-0038-*.md`,
    `docs/ticket-lifecycle.md` and any case-study file against a count taken
    at 8b0a8b4 in the same description — and the total delta.

## Out of scope

- Any change to the tier model itself. The operative test performed correctly
  throughout the source wave; the tiers assigned were right, including two the
  executor raised and the reviewer declined to lower.
- Project-specific lessons from the same wave. Three are being folded into the
  source project's own guidance and do not generalise: a rules-interpretation
  discriminator specific to that ruleset, a PDF-extraction rule about
  case-sensitive search against capitalised headings, and an interim workaround
  for the editable-install hazard pending its own fix. Only the *generalisable*
  form of the third — the no-global-mutation constraint — belongs here.
- Rewriting `README.md`'s summary of the core ideas. If the falsification gate
  deserves to be a seventh core idea, that is a separate judgement and a
  separate ticket.
- The granularity question — whether a defect recurring at many sites should be
  enumerated as a class before being fixed instance by instance. It is a real
  finding from the same wave, but it is a claim about how work is *sized*, it is
  supported by one project's evidence so far, and it would double this ticket.
  Raise it separately if wanted.

## References

- `docs/quality-gates.md` — the coverage rule this ticket qualifies, and the
  identical-script rule it constrains.
- `docs/tier-review-model.md`, ADR-0002 — the countersignature requirement the
  review-yield figure evidences.
- `examples/adr/adr-0038-tickets-carry-the-lineage-of-the-ticket-that-raised-them.md`
  — the pattern corrected here.
- EM-001, `DISCLOSURE.md` — the third-party-material constraint that governs how
  the evidence may be described.

## Notes

**On the review-yield figure.** It is the strongest single number this wave
produced and it wants care. Six of six critical-tier tickets returning findings
at first review is evidence that independent review is not ceremonial; it is not
evidence of a rate that would hold elsewhere, on one project over one wave with
reviewers briefed to look hard. State it with its scope attached or leave it out.

The first draft of this ticket asserted a larger consecutive-review count that
had been carried between agent briefs and never derived from the repository. It
did not survive checking and is corrected in the Context above. It is worth
recording *how* it failed, because the mechanism is the one this ticket
addresses: the number was never wrong at the moment it was first written — it
was inherited, incremented, and restated as fact by successive readers, none of
whom had the source. A measured number and an inherited one are indistinguishable
once written down, which is why the rule has to be that the sentence names the
baseline.

**Placement judgement.** `case-studies/` is the more honest home for the figure
than a policy document, since a policy document that cites its own success rate
reads as advocacy. The implementer may decide otherwise; if so, say why in the
pull-request description.

**On splitting.** The three corrections are urgent in a way the two additions
are not, because the corrected patterns are already published and may be in use.
If the implementer judges this XL rather than L, split along that line —
corrections first — rather than by file. Splitting by file would put the
ADR-0038 annotation and the lifecycle rule in different tickets, and they are
one fact.

**This ticket's own gates.** The repository has no code, so the machine gates do
not apply. The falsification gate applies to it in spirit: for each acceptance
criterion, the reviewer should be able to say what a reader would do differently
because of the change. A guidance edit no reader would act on differently is the
documentation equivalent of a test that cannot fail.

## PR Description

### Ticket
EM-006 — the falsification gate, and three corrections

### Tier
`critical` — process-surface change (clause 5 of the operative test): it
adds a gate, an executor obligation and a reporting rule, and corrects a
published pattern readers may have adopted.

**Independent review obtained**, per ADR-0002: a separate agent, given the
ticket and the diff and not the executor's reasoning, reviewed the change in
two rounds, working read-only. Its findings are recorded under Review below,
and the tree under review was checked clean after each round.

### Summary
Five documents gain the falsification gate and its supporting rules;
ADR-0038 is annotated in place with the two id-namespace defects and their
rules; the ticket lifecycle carries both rules in operational form and states
the subject-length hazard beside the lineage scheme; the review-yield figure
goes in the case study, scoped. One child ticket raised.

### Acceptance criteria
- [x] AC1: coverage measures execution, not discrimination, in its own
  section — `docs/quality-gates.md`, "Coverage measures execution, not
  discrimination", with the inclusive-comparison band and the
  fixture-coincidence mechanism, and the file-at-100% instance.
- [x] AC2: the gate as an executor obligation with a recorded red count, and
  what zero means — `docs/quality-gates.md`, "The falsification gate", steps
  1–3 and the bold sentence on zero.
- [x] AC3: the non-discriminating label and one case per rival — same
  section, the two bullets.
- [x] AC4: baseline-in-sentence required between the policy and the template
  without full duplication — the rule with its reasoning is one bullet in
  `docs/ai-contributor-policy.md` §6; `templates/PR-DESCRIPTION.md` carries a
  one-line pointer to it and a clause in Definition of Done item 9.
- [x] AC5: no-global-mutation with the editable install as the example —
  `docs/quality-gates.md`, "The identical-script rule", the bold paragraph.
- [x] AC6: both namespace defects in the ADR and in the lifecycle —
  `examples/adr/adr-0038-*.md`, "Annotation — added 2026-09-06 under EM-006",
  items 1 and 2 with the placement rule and the next-id rule; the ADR's status
  is unchanged and the diff to it is append-only. `docs/ticket-lifecycle.md`,
  "Lineage", the first two bold paragraphs. The lifecycle's local instance is
  verified: `EM-010-001` was added at 3da6c57 and its file removed at 0947dda,
  and `ls docs/tickets/*/EM-010-*` shows no child of EM-010.
- [x] AC7: subject length does not compose with lineage ids, no rule
  introduced — `docs/ticket-lifecycle.md`, "Lineage", the third bold
  paragraph; `grep -rn "72" docs templates` finds no subject-length rule.
- [x] AC8: no third-party material; DISCLOSURE amended and says why — every
  example is in engineering terms (inclusive comparison, specification
  readings, fixture coincidence, editable install). `DISCLOSURE.md`, "What is
  published", gains a paragraph naming the annotation as the one
  post-publication exception and why it is an annotation rather than a
  supersession; `examples/README.md` says the same in one sentence.
- [x] AC9: independent review — see Review.
- [x] AC10: word counts — `wc -w`, at 8b0a8b4 and at the closing commit of
  this branch:

  | File | 8b0a8b4 | close | Δ |
  |---|---|---|---|
  | `docs/quality-gates.md` | 411 | 1,175 | +764 |
  | `docs/ai-contributor-policy.md` | 1,034 | 1,157 | +123 |
  | `docs/ticket-lifecycle.md` | 544 | 996 | +452 |
  | `templates/PR-DESCRIPTION.md` | 400 | 539 | +139 |
  | `docs/tier-review-model.md` (not edited) | 761 | 761 | 0 |
  | `examples/adr/adr-0038-*.md` | 791 | 1,228 | +437 |
  | `case-studies/00-growth-2024-2026.md` | 641 | 762 | +121 |
  | `DISCLOSURE.md` | 657 | 748 | +91 |
  | `examples/README.md` | 304 | 341 | +37 |

  Total delta across edited files: +2,164 words. The five-document reviewer
  brief the ticket priced at 3,150 words at 8b0a8b4 is 4,628 at close, a 47%
  increase; `docs/quality-gates.md` is 2.9 times its baseline. The ticket
  accepted the cost; this table is what makes it visible.

### Falsification
N/A — no behavioural claim; this repository has no suite. Per the ticket's
Notes, the gate in spirit: what a reader does differently per criterion.
- AC1: stops reading a green coverage delta as evidence a change is pinned.
- AC2–AC3: runs the mutant and writes the count before reporting; keeps and
  labels a test that cannot discriminate; writes one case per rival.
- AC4: writes the baseline in the sentence with the number.
- AC5: builds the gate's environment inside the worktree.
- AC6: creates a review-raised ticket on the branch; reads the next id from
  history. Verified against this repository's own spent id.
- AC7: an adopter with a subject limit decides, instead of discovering.
- AC8: a DISCLOSURE reader knows where the original ADR text stops.

### Out of scope (per ticket)
Confirmed: `docs/tier-review-model.md` is untouched (761 words at 8b0a8b4 and
at close); `README.md` is untouched — the contradiction the gate creates
with its idea 5 is raised as EM-006-001, not fixed; no project-specific
lesson from the source wave was carried over; the granularity question is
left to EM-009, which already exists.

Beyond the Files list and declared here: the `### Falsification` section in
the PR template (required by the gate's own text), one sentence in
`examples/README.md` (required by AC8's honesty about the annotation), and
the local `EM-010-001` instance in the lifecycle (not asked for; verified;
it is the only spent-id measurement this repository can take).

### Placement judgement
The review-yield figure is in the case study, not a policy document, for the
reason the ticket's Notes give: a policy document citing its own success
rate reads as advocacy. It is stated with its scope — one project, one wave,
reviewers briefed to look hard — and with what it does not say.

### Review
Per-round record. The total is derived from the rows, not asserted.

| Round | Must-fix | Where the findings sat | Inside the previous round's fix | Repaired by |
|---|---|---|---|---|
| 1 | 1 (of 10 findings) | documents: 1 must-fix in `examples/README.md`; 9 notes across the ADR annotation, lifecycle, quality-gates, PR template | — | b92c47c |
| 2 | 0 (of 8 notes) | documents: the placement rule's justifying clause stated an unpublished rule as premise; "the source project" still undefined at its first use; three over-long lines; two notes on EM-006-001 as a ticket | 2 of 8 — the premise clause was added in repairing round-1 finding 5, and the template line repairing finding 10 carries a cost the remedy did not price | the closing commit |

Derived total: 1 must-fix over two rounds. Round 1's column-1
findings: the examples README contradicted its own annotated row (must-fix);
the four-changes figure lacked its wave; the README/tier-model contradiction
(raised as EM-006-001). Column-2 findings: the placement rule named no actor;
the next-id command was wrong in one place and printed non-ids in both; three
wording defects in the annotation; "the source project" undefined at first
use; the template gave no line for a change with no behavioural claim. All
nine notes were taken in b92c47c. Round 2's notes were taken in the closing
commit, except one recorded here rather than fixed: the template's line for a
change with no behavioural claim makes the "what a reader does differently"
statement a standing requirement of every documentation-only pull request at
every tier, which is a cost on trivial-tier work that EM-012 is about and
that the round-1 remedy did not price. Post-review tree check after each round:
`git status --porcelain` empty, `git worktree list` showing only the main
tree.

### How to verify
1. `git diff c8c4795..HEAD -- examples/adr/` — the ADR diff is append-only
   below a horizontal rule; nothing above it changed.
2. `git log --diff-filter=A --name-only --format= -- docs/tickets | grep
   EM-010-001` returns the spent id; `ls docs/tickets/*/EM-010-*` does not.
3. `grep -n "Retired when\|same sentence" docs/ai-contributor-policy.md
   templates/PR-DESCRIPTION.md` — the baseline rule once in full, once as a
   pointer.
4. Re-run the `wc -w` table above.

### Risks / follow-ups
- **EM-006-001** (raised here, on this branch, per the placement rule this
  ticket lands): README idea 5 and the tier model's "no tier skips the
  machine checks" are now incomplete.
- The five-document brief grew by 47%. EM-014's cost section already counts
  rules; the word growth is a cost every subsequent reviewer pays.
- The gate is stated for a project with a suite. This repository has none,
  and every ticket here will write `N/A` in Falsification; whether that line
  decays into ceremony is something the maintainer can watch for.

