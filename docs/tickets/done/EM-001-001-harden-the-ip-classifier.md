---
id: EM-001-001
title: Harden the IP classifier and make the triage reproducible
status: done
tier: standard
complexity: M
dependencies: [EM-001]
claimed_by: claude-fable-5-1
claimed_at: 2026-09-06
blocked_at: 2026-09-06
closed_at: 2026-09-15
---

# EM-001-001 — Harden the IP classifier and make the triage reproducible

## Context

Raised while working EM-001. The keyword classifier used to triage 331
artifacts for third-party material **under-flagged**: it cleared 22 tickets
and 7 decision records, of which manual review rejected 15 and 4.

Two specific misses matter:

- A ticket containing a proprietary term inside a type literal in a code
  block. It scored one occurrence; the threshold required two.
- A ticket listing core domain class names in prose. The class names were not
  in the term list at all.

Both would have been published had the cleared set not been read manually.

The classifier was also discarded after use. The triage that gates everything
in this repository is therefore not reproducible, and a reader cannot check
it.

## Specification

Add the classifier to the repository as a runnable script, with the term list
as data rather than embedded literals, and fix the two demonstrated failures.

### Files

- `tools/ip-scan.py` — the classifier
- `tools/terms.txt` — term list, one per line, commented by category
- `tools/README.md` — how to run it and what its output means

### Behaviour

- Any single occurrence of a term flags the file. The two-occurrence
  threshold is removed: it exists only to reduce noise, and the cost of a
  false negative here is publishing someone else's property.
- Code blocks are scanned with the same term list as prose, and reported
  separately so the reader can see where a hit came from.
- Output is a table of file, verdict, matched terms, and location.
- The script exits non-zero if any file in a published directory matches, so
  it can run as a gate.

## Acceptance criteria

1. AC1: Running the script against the current `examples/`, `docs/`,
   `templates/` and `case-studies/` exits zero.
2. AC2: Running it against the two artifacts named in Context flags both.
3. AC3: Removing any term from `terms.txt` and re-running demonstrably
   changes the result, proving the list is data and not hard-coded.
4. AC4: `tools/README.md` states plainly that the script is a filter and not
   a decision, and that its output requires manual review.

## Out of scope

- Re-triaging the source project to publish more artifacts. This ticket makes
  the existing decision reproducible; it does not revisit it.
- Any form of semantic or model-based classification. A keyword scan whose
  limitations are understood and documented is preferable here to a cleverer
  one whose failure modes are not.

## References

- EM-001
- `DISCLOSURE.md`, "How the material was triaged"

## Notes

The finding is already documented in `DISCLOSURE.md` as the substantive lesson
of the triage. This ticket does not change that text — the lesson stands
whether or not the tool improves.

**BLOCKER (2026-09-06):** the executor cannot proceed for two reasons, one an
input and one a decision reserved to the maintainer.

1. **The term list is not available.** Context records that the classifier
   was discarded after use; the term list exists, if at all, only on the
   maintainer's machine. Without it AC1 is vacuous (an empty list clears
   everything), AC3 cannot be demonstrated, and AC2 depends on two private
   artifacts that are not in this repository and cannot be.
2. **Whether `tools/terms.txt` may be published is a publication decision the
   ticket does not make.** A list of a third party's vocabulary identifies the
   ruleset, which is the domain content `DISCLOSURE.md` withholds. The ticket
   specifies the list as data in the tree without saying whether the tree it
   means is the public one. Options the executor can see: publish the list
   (maintainer's call, with the disclosure amended to say why a vocabulary is
   not content); ship the script with the list gitignored and a documented
   format, so AC1–AC3 are verified by the maintainer locally and the README
   says so; or a decoy list that proves the mechanism and nothing else.

To proceed the executor needs the maintainer's choice among those, and, for
the first two, the list — or the two artifacts named in Context, or a stated
substitute for AC2.

## Maintainer decision (2026-09-15)

**BLOCKER DISCHARGED.** The maintainer answered by closing the ticket rather
than by answering either question it raised: no classifier is added to this
repository. Item 2's publication question does not arise, because nothing is
published. Item 1's missing term list does not arise, because nothing would
consume it.

The reason is a constraint this ticket's Specification contradicts. This
repository publishes process, not product, as `DISCLOSURE.md` and the README
both say, and it carries no runnable tooling. The Specification is
`tools/ip-scan.py` and `tools/terms.txt` and nothing else, so no part of the
ticket survives the constraint and could be worked as written. Respecifying it
without a script was offered and declined.

What the ticket recorded is not withdrawn. The classifier under-flagged, and
the triage that cleared this repository's published artifacts is not
reproducible from this repository. That is now an accepted risk, carried in
Risks / follow-ups below, rather than a defect this repository will repair.

## PR Description

### Ticket
EM-001-001 - Harden the IP classifier and make the triage reproducible.

### Tier
`trivial`. The frontmatter's `standard` priced the script and the term list
the Specification asks for, and neither is written. What this change touches
is this ticket file, one row of `docs/tickets/README.md`, and one new ticket
file - "ticket edits" in the tier table's `trivial` row, which summons no
independent pass. None was run. The board file states rules as well as
carrying the board, but the rule-stating text is untouched here; only a
record changes, and the tier model is explicit that a record of work is not
a process document.

### Summary
EM-001-001 closes without the work it specifies. The maintainer's decision of
2026-09-15 is that no classifier script enters this repository, which leaves
the ticket with an empty Specification rather than an unanswered question.

### Acceptance criteria
Every criterion names the script or the term list, and neither exists. None is
met, and none is to be met; the ticket closes on the decision above, not on
the criteria.
- [ ] AC1: running the script against `examples/`, `docs/`, `templates/` and
  `case-studies/` exits zero - no script; not met.
- [ ] AC2: running it against the two artifacts named in Context flags both -
  no script, and the artifacts are private and outside this repository; not
  met.
- [ ] AC3: removing a term from `terms.txt` changes the result - no term list;
  not met.
- [ ] AC4: `tools/README.md` states the script is a filter and not a decision
  - no `tools/` directory; not met.

### Falsification
N/A - this change makes no behavioural claim. Per criterion, what a reader
does differently because of it: a reader looking for the classifier learns
from this record that it is deliberately absent and why, rather than finding a
blocked ticket that implies it is merely pending.

### Out of scope (per ticket)
Nothing here exceeds the ticket's scope; it falls short of it by decision.
- Re-triaging the source project. Untouched, as the ticket already excluded.
- Any semantic or model-based classification. Untouched.
- Respecifying reproducible triage without a script. Offered to the maintainer
  and declined; not carried to a follow-up.

### How to verify
1. `git show HEAD --stat` names only ticket files and the board.
2. `ls tools 2>/dev/null` finds nothing; the repository carries no script.
3. `grep -rn 'ip-scan' --include=*.md .` returns only this ticket's own text.

### Risks / follow-ups
- **Accepted risk.** The triage that cleared this repository's artifacts is
  not reproducible from this repository, and its classifier is known to have
  under-flagged. Anyone auditing the disclosure has the maintainer's word and
  the result, not the mechanism. The maintainer accepts this in closing the
  ticket.
- **Follow-up raised.** EM-001-001-001, for a lifecycle gap this closure
  exposed: "Closing" describes a ticket that was worked, and there is no
  written path for one that will not be. This ticket took the `done/` path
  because it is the only close the directory/status invariant offers.

### Review
N/A - `trivial` tier, and not a change to a process document.
