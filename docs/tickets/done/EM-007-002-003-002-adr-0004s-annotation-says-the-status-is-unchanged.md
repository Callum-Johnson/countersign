---
id: EM-007-002-003-002
title: ADR-0004's annotation says the status is unchanged and the status has changed
status: done
tier: standard
kind: defect
impact: degraded
delivery: maintenance
why: "Without correcting it, ADR-0004 states in its own text that its status is unchanged while the line above carries a changed value, and nothing in the file lets a reader order the two."
complexity: S
dependencies: [EM-007-002-003-001]
claimed_by: claude-opus-5
claimed_at: 2026-09-15
closed_at: 2026-09-15
blocked_at:
closed_at:
---

# EM-007-002-003-002 — ADR-0004's annotation says the status is unchanged

## Why this ticket should be worked

The affected outcome is whether ADR-0004 can be read without the reader having
to guess which of two sentences is current.

Its 2026-09-15 annotation opens: "Not part of the decision as recorded. The
text above the horizontal line is unchanged, and the status is unchanged."
EM-007-002-003-001 changed the status from `proposed` to `accepted` on the
same date, above that rule. The record now carries both.

The sentence has two readings and the file supports neither over the other.
Narrowly it describes what the annotation did — that annotation did not change
the status, which is true and stays true. Broadly it is a standing claim about
the record, which is now false. The sibling preambles on ADR-0001 and ADR-0002
say "the status stays `accepted`", which is unambiguously the broad reading
and remains true of those records; ADR-0004's wording is the one that does not
describe its own file.

Deferring this leaves a self-contradicting record whose subject is the tier of
every process-document change — the record contributors reach for most. It is
`degraded` rather than blocking because the status line itself is correct and
the decision is untouched; only the annotation's description of the file is
stale.

## Context

Raised by the one independent review pass on EM-007-002-003-001 (finding
R1.2), which recorded it and routed it rather than repairing it: the remedy
lies inside that ticket's own stated limits — Behaviour, "The body of the
record and its annotation are untouched", and Out of scope, "any part of its
body" — so under the second condition of "When review ends" it goes to a
ticket that owns it, raised because none existed.

## Specification

Documentation change only.

### Files

- `docs/adr/0004-a-process-document-change-is-standard-on-one-pass.md`, the
  2026-09-15 annotation's preamble, or a new annotation below it.

### Public surface

N/A — this repository publishes documents.

### Behaviour

- The record no longer asserts that its status is unchanged while carrying a
  changed one.
- Whichever form is chosen, the 2026-09-15 annotation's substance is not
  rewritten: either its preamble gains a clause naming the later transition
  and the ticket that made it, or a new dated annotation below its own rule
  records the transition. A dated annotation is not edited to say something
  it did not say, per EM-023-001.
- The wording chosen says which of the two readings the preamble carries, so
  the next annotation on any record has one form to copy.

## Acceptance criteria

1. AC1: no sentence in ADR-0004 claims the status is unchanged while the
   status line reads a value it did not carry when that sentence was written.
2. AC2: the 2026-09-15 annotation's substance is unchanged; any addition is a
   clause naming the transition, or a new annotation below a rule of its own.
3. AC3: the preambles of the annotations on ADR-0001, ADR-0002, ADR-0003 and
   ADR-0004 are compared, and the description says whether they now state the
   same thing the same way or whether a further ticket is owed.
4. AC4: a change to a process document is `standard` on one independent
   review pass, per "The operative test"; the pass is recorded as one row of
   the Review table.

## Out of scope

- The status value itself, which EM-007-002-003-001 settled, and the decision
  ADR-0004 records.
- Any other record's annotation, except to read it for AC3.

## References

- `docs/adr/0004-...md`, the 2026-09-15 annotation.
- EM-007-002-003-001, Review, R1.2 — the finding this is routed from.
- EM-023-001 — that a dated annotation is appended to, never edited.
- ADR-0001 and ADR-0002, whose preambles use "the status stays `accepted`".

## Notes

The id was read with the next-id command as EM-023 corrected it: `git log
--full-history --diff-filter=AR --name-only --format= -- docs/tickets`, with
the EM-007-002-003 children extracted, returns `EM-007-002-003-001` alone.

## PR Description

### Ticket
EM-007-002-003-002 — ADR-0004's annotation says the status is unchanged and
the status has changed.

### Tier
`standard`, on one independent review pass. A decision record under
`docs/adr/` is a process document under "The operative test". The pass ran
against 2eb7e7d and is row 1 of the Review table.

### Summary
ADR-0004's 2026-09-15 annotation opened "the text above the horizontal line is
unchanged, and the status is unchanged", and EM-007-002-003-001 moved the
status above that rule on the same date. The preamble now states what is true
of each: unchanged *by this annotation*, and the status read `proposed` when
the annotation was written and moved the same day, with the ticket that moved
it named. The annotation's findings are untouched.

### Acceptance criteria
- [x] AC1: no sentence in ADR-0004 claims the status is unchanged while the
  status line reads a value it did not carry when that sentence was written.
  The relative claim is gone; sentence 1 is scoped to the annotation's own act
  and sentence 2 is historical. `grep -n "status is unchanged\|status stays"
  docs/adr/0004-a-process-document-change-is-standard-on-one-pass.md` returns
  nothing. Two neighbouring unchanged-status claims elsewhere in the file, in
  Decision and Migration, are about ADR-0002 and ADR-0003, both still
  `accepted`, so both remain true.
- [x] AC2: the annotation's substance is unchanged. Word by word, the whole
  change is inside the blockquote: "Not part of the decision as recorded" is
  identical; "The text above the horizontal line is unchanged" gains "by this
  annotation" and loses ", and the status is unchanged"; two sentences are
  added naming the transition and the ticket that amended the preamble.
  Everything below the blockquote — the clause-5 quotations and the four
  sentences of finding — is byte-identical.

  **The deletion, and its grounds.** AC2's wording sanctions "a clause naming
  the transition"; the change also deletes five words, which that wording does
  not by itself authorise. The grounds are stated here rather than left
  implicit: AC1 cannot be discharged by appending alone, because a new
  annotation below its own rule would leave "the status is unchanged" standing
  in the 2026-09-15 preamble, which is exactly what AC1 forbids. The two arms
  the ticket offers are not equivalent, and only one meets both criteria.
- [x] AC3: the preambles are compared, and a further ticket **is** owed. There
  are six annotations across the four records, not five — ADR-0002 carries
  three, and its middle one has no preamble at all.

  | Record / annotation | Preamble, verbatim |
  |---|---|
  | ADR-0001, 2026-09-06 under EM-017 | "Not part of the decision as recorded. The text above the horizontal line is unchanged, and the status stays `accepted`." |
  | ADR-0002, 2026-09-06 under EM-010-002 | "This section is not part of the decision as recorded. Everything above the horizontal line is the original text, and the status is unchanged." |
  | ADR-0002, 2026-09-06 under EM-017 | *none — the section opens straight onto its body* |
  | ADR-0002, 2026-09-10 under EM-007-002 | "Not part of the decision as recorded. The text above the horizontal line is unchanged, and the status stays `accepted`." |
  | ADR-0003, 2026-09-10 under EM-007-002 | "Not part of the decision as recorded. The text above the horizontal line is unchanged, and the status is unchanged." |
  | ADR-0004, 2026-09-15, as amended here | "Not part of the decision as recorded. The text above the horizontal line is unchanged by this annotation. The status read `proposed` when this annotation was written and was moved to `accepted` the same day, under EM-007-002-003-001, which was the transition `docs/adr-process.md` then required once a record's change had merged. This preamble was amended on the same date under EM-007-002-003-002 …" |

  They do not state the same thing the same way: four forms plus one absence,
  varying on the opener, the assurance and the status clause. No record is
  false today — neither ADR-0002's nor ADR-0003's status has moved since its
  annotation — but the relative form that this ticket found has two readings
  still stands in two places, and it fires the moment one of those records
  transitions. **EM-007-002-003-002-001 is raised for them**, and for the
  canonical form: this change introduced a fourth wording, specific to
  ADR-0004, that no other annotation can copy, so settling the form is part of
  that ticket rather than only correcting the two stale ones.
- [x] AC4: a change to a process document is `standard` on one independent
  review pass. The pass ran against 2eb7e7d by an agent that did not perform
  the work and did not receive the executor's reasoning, and is row 1 of the
  Review table below. It returned two must-fixes over four findings, both
  repaired.

### Falsification
N/A for a behavioural claim — this repository publishes documents and runs no
suite. Per criterion, what a reader does differently: a reader of ADR-0004's
annotation is told what the status read when it was written and what moved it,
instead of reading that the status is unchanged beside a status line that has
changed.

For the must-fixes repaired, per the contributor policy's §6:

- R1.2 — class: **which sentences does this heading now attribute to a ticket
  that could not have written them?** The two added sentences are the
  instance. The question was asked of every sentence under the 2026-09-15
  heading. Siblings, each checked:
  - **The two sentences naming the transition** — the instance. They name
    EM-007-002-003-001, whose work commit and ticket file both postdate the
    commit that wrote this annotation, so the heading "added 2026-09-15 under
    EM-007-002-003" credited that ticket with text it could not have written.
    Repaired: the preamble says it was amended on the same date under
    EM-007-002-003-002, and why it names a later ticket.
  - **"unchanged by this annotation"** — checked; it is a narrowing of a
    sentence EM-007-002-003 did write, and the amendment is now declared, so
    the attribution reads correctly.
  - **The findings below the blockquote** — checked and byte-identical, so
    they remain EM-007-002-003's in fact as well as by heading.
  What a reader does differently: a reader tracing provenance finds which
  ticket wrote which sentence, rather than attributing to EM-007-002-003 a
  statement about a ticket raised after it finished.
- R1.1 — class: **which criteria does this change assert as met with the
  evidence living nowhere in the tree?** AC3's comparison is the instance —
  the same class EM-007-002-003-001's own R1.1 repaired one ticket earlier in
  this lineage. Asked of all four criteria: AC1 and AC2 name commands and the
  diff, AC4 is discharged by the pass whose row is below, and AC3's comparison
  now exists above with all six preambles quoted.
- R1.3 — note. Repaired: "which is the transition `docs/adr-process.md`
  requires" was present-tense about a rule carrying its own **Retired when:**,
  so it would go stale if that section were amended — the very class this
  lineage exists to close. It now reads "was the transition … then required".
- R1.4 — note. Repaired by the AC2 grounds paragraph above.

### Out of scope (per ticket)
Confirmed; nothing exceeds it.
- The status value, which EM-007-002-003-001 settled — untouched; it is not
  even a context line in the diff.
- The decision ADR-0004 records — untouched.
- Any other record's annotation except to read it for AC3 — ADR-0001,
  ADR-0002, ADR-0003 and ADR-0005 are outside the commit, and were opened only
  to be read.

### How to verify
1. `sed -n '/^## Annotation — added 2026-09-15/,+12p' docs/adr/0004-a-process-document-change-is-standard-on-one-pass.md`
   — the preamble as it stands.
2. `grep -n "status is unchanged\|status stays" docs/adr/0004-a-process-document-change-is-standard-on-one-pass.md`
   — nothing, which is AC1.
3. `git diff main...HEAD --name-only` — the record, the ticket file, the new
   ticket and the board row; no other record and not `docs/adr-process.md`.
4. Read the AC3 table against the four records and check each quotation.

### Risks / follow-ups
- **On EM-023-001, which this change appears to cut against.** That ticket
  established that a dated annotation is appended to, never edited. This change
  edits one. The grounds, stated so a reader can disagree with them: the
  dateline is not falsified, because every word under the 2026-09-15 heading
  was in fact written on 2026-09-15, where EM-023-001's instance put text
  written on 2026-09-15 under a 2026-09-06 dateline; what was edited is the
  preamble's disclaimer about the file's state, not the record of what was
  found, which is what EM-023-001's instance altered; and AC1 cannot be met by
  appending alone. EM-023-001 deliberately did not write its practice into
  `docs/` — it is a recorded practice with two instances, not a rule with a
  falsifier — so this is a reading of that practice and not an exception to a
  rule. If a maintainer reads it the other way, the remedy is a new annotation
  and the deletion reversed, and EM-007-002-003-002-001 is where that would be
  settled.
- The amended preamble is a fourth form. It is record-specific and no other
  annotation can copy it, which is the second half of what
  EM-007-002-003-002-001 owns.

### Review
One independent review pass, per "The operative test" for a change to a
process document. No second pass is taken.

| Round | Must-fix | Where (rules / lists / documents / tests) | Inside previous round's fix | Repaired by |
|---|---|---|---|---|
| 1 | 2 (of 4 findings) | documents: AC3's whole deliverable — the comparison of the annotation preambles — existed nowhere in the tree, the same class the previous ticket in this lineage repaired (must-fix); the 2026-09-15 heading attributed to EM-007-002-003 two sentences naming a ticket raised after that ticket finished (must-fix); the new preamble carried a present-tense claim about a rule in `docs/adr-process.md` that carries its own Retired-when, so it could go stale; the deletion of five words from a dated annotation was made without its grounds stated anywhere in the tree | — | this commit |

Derived from the row and not asserted beside it: two must-fixes over one
review round, both repaired. Round 1 has no round before it, so its
inside-previous-fix cell reads `—` and no line is uncountable.

- R1.1 · permits · must-fix · `docs/ai-contributor-policy.md` §6, "Every acceptance criterion met and demonstrated in the pull-request description, with evidence" · AC3's entire deliverable is a comparison of the annotation preambles, and none existed in the change — the ticket's description was the authoring placeholder and the commit message named no other record — remedy: write the comparison into the description, quoting all six preambles and naming the records a further ticket is owed for; cost, if the remedy tightens a control: none, it supplies evidence the criterion already names; inside previous fix: —
- R1.2 · permits · must-fix · `docs/adr/0004-...md`, the heading "## Annotation — added 2026-09-15 under EM-007-002-003" · the preamble under it carried two sentences naming EM-007-002-003-001, whose work commit and ticket file both postdate the commit that wrote the annotation, so the heading attributed to one ticket text authored under another and EM-007-002-003-002 appeared nowhere in the record — remedy: one clause saying the preamble was amended the same date under EM-007-002-003-002; cost: none; inside previous fix: —
- R1.3 · permits · note · `docs/adr/0004-...md`, "which is the transition `docs/adr-process.md` requires once a record's change has merged" · a present-tense claim about another document's current rule, planted in a dated annotation, where that rule carries its own Retired-when — the class this lineage exists to close — remedy: past-tense or date-anchor it; cost: none; inside previous fix: —
- R1.4 · permits · note · EM-023-001, and `DISCLOSURE.md`, "because a dated annotation records what was found on its date" · the change deletes words a dated annotation carried instead of appending, and stated its grounds nowhere in the tree — remedy: state the grounds in the description; cost: none; inside previous fix: —

The reviewer found nothing in the second column and recorded that as an
answer: the change adds no rule, no list entry and no refusal, removes no path
a contributor uses, and leaves ADR-0004 open to supersession. No tightening
occurred, so no cost line is owed, and none of the first-column remedies adds
a control.

### Definition of Done (all tiers)
The four machine checks do not apply to a repository that publishes documents
and runs no suite; the falsification gate is discharged above, with N/A for
the behavioural claim and a class line per must-fix repaired. Every measured
figure names its baseline in the same sentence and is read from the command
named beside it. The independent pass a process-document change takes has run
and is recorded.
