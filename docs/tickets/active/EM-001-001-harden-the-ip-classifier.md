---
id: EM-001-001
title: Harden the IP classifier and make the triage reproducible
status: in-progress
tier: standard
complexity: M
dependencies: [EM-001]
claimed_by: claude-fable-5-1
claimed_at: 2026-09-06
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
