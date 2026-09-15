---
id: EM-023-002
title: The disclosure counts one post-publication annotation and there are now two
status: done
tier: trivial
kind: defect
impact: degraded
delivery: maintenance
why: "Without correcting the count, DISCLOSURE.md and the examples README state a false fact about what was added to a published artifact, and those two files are the whole of this repository's claim about the integrity of its evidence."
complexity: S
dependencies: [EM-023-001]
claimed_by: claude-opus-5
claimed_at: 2026-09-15
blocked_at:
closed_at: 2026-09-15
---

# EM-023-002 — The disclosure counts one post-publication annotation

## Why this ticket should be worked

The affected outcome is whether this repository's account of its own evidence
is true.

`DISCLOSURE.md` said "One exception was made after publication and is marked
as such", and `examples/README.md` said "One dated annotation was added later,
under its own heading, to `adr-0038`". EM-023-001 added a second dated
annotation to that file on 2026-09-15. Both sentences became false at that
commit.

That matters more than its size. The argument DISCLOSURE.md makes is that the
published artifacts are genuine and that every departure from what was
published is named — "Where an artifact needed redaction to be publishable, it
was excluded rather than redacted". A reader checks that argument by counting
the named exceptions against the file. Until this ticket, the count did not
match: `grep -c 'Annotation — added' examples/adr/adr-0038-tickets-carry-the-lineage-of-the-ticket-that-raised-them.md`
returns 2 and both documents said one.

Deferral is not acceptable while the defect is on the default branch, because
the false sentence is the one a sceptical reader is most likely to test.

## Context

Raised while working EM-022-001, on reading `DISCLOSURE.md` to check whether
that ticket's Specification was compatible with the claims made about the
published examples. The defect was introduced by EM-023-001, whose Out of
scope reasoned that with the 2026-09-06 text restored both documents "read
true again". That reasoning covered the restoration and missed the addition:
restoring the earlier annotation made "nothing within a published file was
changed" true again, while the new annotation made "one annotation" false.

## Specification

Documentation change only.

### Files

- `DISCLOSURE.md`, the post-publication exception paragraph.
- `examples/README.md`, the intro sentence and the `adr-0038` table row.

### Public surface

Both files are this repository's statement to a reader about what its evidence
is. That statement is the surface.

### Behaviour

- Both documents state the number of post-publication annotations that the
  file actually carries, and name each by date and ticket.
- `DISCLOSURE.md` states that the earlier annotation is unchanged as well as
  the original text, and why a second annotation was added rather than the
  first edited.
- Neither document acquires a count that its own sentence does not determine;
  each names the annotations rather than asserting a total separately from
  them.

## Acceptance criteria

1. AC1: the number of post-publication annotations stated in `DISCLOSURE.md`
   and in `examples/README.md` equals the number in the file, read from a
   command.
2. AC2: each annotation is named by its date and its ticket in
   `DISCLOSURE.md`.
3. AC3: `DISCLOSURE.md` states that the earlier annotation is unchanged, and
   why the second was appended rather than the first amended.
4. AC4: nothing else in either document changes.

## Out of scope

- `examples/adr/adr-0038-...md` itself. EM-023-001 owns its content and
  closed; this ticket only corrects what other documents say about it.
- Any change to the exclusion-rather-than-redaction policy.

## References

- `DISCLOSURE.md` — the post-publication exception paragraph.
- `examples/README.md` — the intro sentence and the table row.
- EM-023-001 — the ticket that added the second annotation and whose Out of
  scope missed this.
- EM-023 — the ticket whose repair started the sequence.

## Notes

N/A.

## PR Description

### Ticket
EM-023-002 — The disclosure counts one post-publication annotation and there
are now two.

### Tier
`trivial`. Neither file states a rule a contributor follows or a procedure a
contributor performs: `DISCLOSURE.md` says what was withheld and why, and
`examples/README.md` says what the published artifacts are. "The operative
test" reaches a process document under `docs/` or `templates/` that states
rules, every document the contributor policy's map names, and a decision
record under `docs/adr/`; these are none of those, and the `trivial` line
reaches documentation other than a process document. The tier table gives
`trivial` no independent pass and the author self-merges. The reasoning is
stated so a reader who places the line elsewhere can see which sentence was
relied on.

### Summary
EM-023-001 added a second dated annotation to `adr-0038`, which made the
"one exception" sentence in `DISCLOSURE.md` and the "one dated annotation"
sentence in `examples/README.md` false. Both now name both annotations, by
date and ticket, and `DISCLOSURE.md` records why the second was appended
rather than the first amended.

### Acceptance criteria
- [x] AC1: the stated number matches the file. `grep -c 'Annotation — added'
  examples/adr/adr-0038-tickets-carry-the-lineage-of-the-ticket-that-raised-them.md`
  returns 2, run after the repair commit on this branch, and both documents
  now say two. Neither asserts the total apart from the annotations it names:
  each sentence lists them, so the list is the count.
- [x] AC2: both are named by date and ticket — 2026-09-06 under EM-006, and
  2026-09-15 under EM-023 — in `DISCLOSURE.md`'s exception paragraph.
- [x] AC3: `DISCLOSURE.md` states that the original text above both
  annotations is unchanged and that the earlier annotation is unchanged too,
  gives the reason a dated annotation is not edited, and records that EM-023
  first edited it in place and EM-023-001 restored it.
- [x] AC4: nothing else changes. `git diff main...HEAD --stat` names
  `DISCLOSURE.md`, `examples/README.md`, this ticket file and the board, and
  the two document diffs are confined to the exception paragraph, the intro
  sentence and the `adr-0038` row.

### Falsification
N/A for a behavioural claim — this repository publishes documents and runs no
suite. Per criterion, what a reader does differently: a reader checking
DISCLOSURE.md's integrity argument by counting the named exceptions against
the file finds the two agree, instead of finding a document that understates
what was added to its own evidence.

No review finding is repaired: this ticket carries no review round, and the
defect was found by the executor.

### Out of scope (per ticket)
Confirmed. `adr-0038` itself is untouched — `git diff main...HEAD --
examples/adr/` is empty. The exclusion-rather-than-redaction policy is
unchanged.

### How to verify
1. `grep -c 'Annotation — added' examples/adr/adr-0038-tickets-carry-the-lineage-of-the-ticket-that-raised-them.md`
   — returns 2.
2. `sed -n '/^Two exceptions were made after publication/,/may not open./p' DISCLOSURE.md`
   — both annotations named by date and ticket, with the reason.
3. `sed -n '7,10p' examples/README.md` — the corrected intro sentence.
4. `git diff main...HEAD -- examples/adr/` — empty, which is Out of scope.

### Risks / follow-ups
- **The pattern, recorded.** This is the third correction in one sequence:
  EM-023 edited a dated annotation in place, EM-023-001 restored it and added
  one below, and this ticket fixes the two documents that counted them. Each
  step was found by reading the next document out rather than by a reviewer.
  What it costs is three tickets for one correction; what it buys is that
  every claim about the published artifacts is now checkable by a command,
  which is what the second How-to-verify step is.
- A count of post-publication annotations lives in two documents and is
  determined by a third file. Neither document now asserts a bare total —
  each names the annotations — which is the form "A number determined
  elsewhere has one site that goes red" asks for where a project has no
  suite. A third annotation would still require editing both documents, and
  there is no site that goes red if it does not. That is one instance; a
  second would clear the bar in "A rule needs a second instance" for doing
  something about it.

### Review
N/A — `trivial` tier, and not a change to a process document.
