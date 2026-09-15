---
id: EM-023-001
title: The ADR-0038 correction rewrote a dated annotation instead of adding one
status: done
tier: trivial
kind: defect
impact: degraded
delivery: maintenance
why: "Without restoring it, a dated annotation in a published artifact says something different from what it said on its date, and this repository's claim that its examples are unaltered records is false."
complexity: S
dependencies: [EM-023]
claimed_by: claude-opus-5
claimed_at: 2026-09-15
blocked_at:
closed_at: 2026-09-15
---

# EM-023-001 — The ADR-0038 correction rewrote a dated annotation

## Why this ticket should be worked

The affected outcome is whether a dated record in this repository means what
its dateline says.

`examples/adr/adr-0038-...md` carries an annotation headed "added 2026-09-06
under EM-006", whose own preamble says everything above its horizontal line is
the original text. Inside that annotation is a *Next-id rule* with a command.
EM-023 corrected the command by editing it in place, at c6943db. The
annotation now reports, under a 2026-09-06 dateline, a command that was not
written until 2026-09-15.

Deferring this leaves two things wrong. The dateline is false, which is the
failure every annotation in this repository exists to avoid — ADR-0002,
ADR-0003 and ADR-0004 are each corrected by a *new* dated annotation with the
earlier text untouched, and EM-007-002-003 added the most recent one nine
commits before EM-023 did the opposite. And `examples/README.md` states that
"nothing else was changed at publication, and nothing within a published file
is redacted", naming the single 2026-09-06 annotation as the one addition;
an in-place edit to that annotation's content makes the sentence untrue.

The evidence is the diff: `git show c6943db -- examples/adr/adr-0038-tickets-carry-the-lineage-of-the-ticket-that-raised-them.md`
is a one-line replacement inside the annotation, not an addition after it.

Deferral is not acceptable while EM-023 is merged, because the defect is live
on the default branch.

## Context

Raised immediately after EM-023 closed, by its own executor reading the file
it had edited. The finding is not the reviewer's; the round-1 pass correctly
identified that the stale command in ADR-0038 was a sibling of the class and
should be repaired, and said nothing about the mechanism. The mechanism was
the executor's choice and it was the wrong one.

## Specification

Documentation change only.

### Files

- `examples/adr/adr-0038-tickets-carry-the-lineage-of-the-ticket-that-raised-them.md`

### Public surface

The file is a published artifact. Its integrity as a record is the surface.

### Behaviour

- The 2026-09-06 annotation reads exactly as it did before c6943db.
- A new annotation, dated and attributed, carries the correction EM-023 made,
  in the form ADR-0002, ADR-0003 and ADR-0004 carry.
- The new annotation says that the earlier one was edited in place and
  restored, so the correction of the correction is itself in the record.

## Acceptance criteria

1. AC1: the 2026-09-06 annotation's command is byte-identical to its state at
   `c6943db^`.
2. AC2: a new annotation, below its own horizontal rule, carries the
   corrected command and names its date and ticket.
3. AC3: both commands in the file run as printed and return what the file
   says they return.
4. AC4: nothing above the new annotation's horizontal rule changes.

## Out of scope

- Any further change to the next-id rule itself. EM-023 owns the rule; this
  ticket owns only how its correction was recorded here.
- `examples/README.md` and `DISCLOSURE.md`, which describe this file. With
  the annotation restored and the correction added below a rule, both read
  true again, so neither needs amending. Had the in-place edit stood, they
  would have.

## References

- `examples/adr/adr-0038-...md` — the record.
- EM-023, Falsification, R1.2 — the finding whose repair chose the wrong
  mechanism.
- `examples/README.md` — the claim the in-place edit falsified.
- ADR-0002, ADR-0003, ADR-0004 — the annotation form this repository uses.

## Notes

This is the second instance in this repository of a later ticket needing to
correct words an earlier record quotes; EM-007-002-003's Risks section
recorded the first and noted that a second would clear the bar "A rule needs
a second instance" sets. It is recorded here as that second instance. Writing
the practice down — that a dated annotation is never edited, only followed by
another — is not done here, because that is a rule entering the documents and
belongs in a ticket of its own rather than in the ticket that met the
instance.

## PR Description

### Ticket
EM-023-001 — The ADR-0038 correction rewrote a dated annotation instead of
adding one.

### Tier
`trivial`. `examples/adr/` holds published artifacts of another project, not
process documents of this one: "The operative test" lists a document under
`docs/` or `templates/` that states rules a contributor follows, every
document the contributor policy's map names, and a decision record under
`docs/adr/`. This file is none of those, and the test's `trivial` line reaches
documentation other than a process document. The tier table gives `trivial`
no independent pass and the author self-merges. The reasoning is stated here
rather than assumed so that a reader who thinks the line falls elsewhere can
see exactly which sentence was relied on.

### Summary
EM-023 corrected a stale command inside ADR-0038's 2026-09-06 annotation by
editing it in place, which made that annotation's dateline false. The original
text is restored and the correction moved to a new dated annotation below its
own horizontal rule.

### Acceptance criteria
- [x] AC1: the 2026-09-06 annotation's command is byte-identical to its state
  before the edit — `git diff c6943db^ HEAD -- examples/adr/adr-0038-tickets-carry-the-lineage-of-the-ticket-that-raised-them.md`
  shows no change within that annotation; the only difference from `c6943db^`
  is the new section appended at the end.
- [x] AC2: a new annotation, below its own horizontal rule, carries the
  corrected command and names its date and ticket — "Annotation — added
  2026-09-15 under EM-023", with a preamble saying that everything above the
  rule is unchanged including the 2026-09-06 annotation.
- [x] AC3: both commands run as printed. Against a history where
  `PRJ-028-first.md` is renamed to `PRJ-029-first.md`, the 2026-09-06 form
  returns `PRJ-028` and the 2026-09-15 form returns `PRJ-028` and `PRJ-029`,
  which is what the new annotation says of them. Both were run with their sed
  and `sort -u` exactly as printed.
- [x] AC4: nothing above the new annotation's horizontal rule changes — the
  diff against `c6943db^` is one appended section and nothing else.

### Falsification
N/A for a behavioural claim — this repository publishes documents and runs no
suite. Per criterion, what a reader does differently: a reader of the
2026-09-06 annotation gets the command that annotation actually gave on that
date, and finds the later correction where later corrections go, so the file
can be read as a sequence of dated findings rather than as a single text
someone keeps editing.

No review finding is repaired here: this ticket carries no review round, and
the defect was found by the executor rather than by a reviewer.

### Out of scope (per ticket)
Confirmed.
- The next-id rule itself — untouched. The command in the new annotation is
  the one EM-023 landed, quoted, not revised.
- `examples/README.md` and `DISCLOSURE.md` — untouched, and now true again.

### How to verify
1. `git diff c6943db^ HEAD -- examples/adr/adr-0038-tickets-carry-the-lineage-of-the-ticket-that-raised-them.md`
   — one appended section; nothing inside the 2026-09-06 annotation.
2. `grep -n 'diff-filter' examples/adr/adr-0038-tickets-carry-the-lineage-of-the-ticket-that-raised-them.md`
   — two commands, the 2026-09-06 one reading `--diff-filter=A` and the
   2026-09-15 one reading `--full-history --diff-filter=AR`.
3. Build the AC3 history — `git init`, commit
   `docs/tickets/ready/PRJ-028-first.md`, `git mv` to `PRJ-029-first.md`,
   commit — and run both commands as printed.

### Risks / follow-ups
- **Recorded, not raised.** This is the second instance of a later ticket
  needing to correct words an earlier record quotes, after the one
  EM-007-002-003 recorded. The bar in "A rule needs a second instance" is
  therefore met for a rule saying a dated annotation is never edited in place.
  The rule is not written here, because writing it is a ticket's own subject
  and this ticket met the instance rather than owning the rule.
- EM-023's own description records the ADR-0038 edit under "Departure from
  Files, recorded". That record stands and is not rewritten; it describes what
  that ticket did, which is what a closed record is for. This ticket is where
  the correction lives.

### Review
N/A — `trivial` tier, and not a change to a process document.
