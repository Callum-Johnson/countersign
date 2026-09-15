# Disclosure policy

What this repository deliberately does not contain, and the reasoning.

## The short version

The projects this methodology was developed on are private. Two of them
implement a ruleset owned by a third party. This repository publishes the
process I built around that work — templates, policies, workflow rules — and
withholds the work itself.

No source code, no rules content, no game data, no product internals.

## How the material was triaged

Before publishing anything I assessed every architecture decision record and
every closed ticket in the largest project against one test: **does this
artifact describe a third party's intellectual property, or only my own
engineering process?**

It took two passes, and the second one mattered.

**Pass one — automated.** A keyword classifier scored each file for
domain vocabulary, rules citations and quoted rule text. It cleared 22 of 292
tickets and 7 of 39 decision records.

**Pass two — manual review of everything the classifier cleared.** It had
under-flagged. Two tickets it passed contained domain terms inside code
snippets — a type literal enumerating rules concepts, and a list of core
domain classes — that the scoring missed because each file contained only a
single occurrence and the threshold required two. Several others carried heavy
mechanics vocabulary in prose that individually scored below the line.

Final position:

| Artifact type | Total | Cleared by classifier | Published after review |
|---|---|---|---|
| Architecture decision records | 39 | 7 | **3** |
| Closed tickets | 292 | 22 | **7** |

Ten artifacts out of 331. That is the expected result when a project
implements someone else's ruleset: the engineering decisions and the rules
content are entangled at the sentence level, and most artifacts cannot be
separated from the domain without being rewritten into fiction.

The lesson is recorded here rather than quietly fixed, because it is the
substantive one: **an automated content scan is a filter, not a decision.** It
narrowed 331 files to 29 for me to read. It was wrong about 19 of them.

## What is published

- **Templates** — the decision-record, ticket and pull-request templates.
  Structure, not content.
- **Policy documents** — the AI contributor policy, ticket lifecycle, tier
  review model, quality gates and decision-record process, distilled from the
  working versions.
- **Ten real artifacts** — three decision records and seven tickets, chosen
  because they concern software architecture and workflow only: API shape,
  CORS, packaging, CI configuration, and fixes to the ticket process itself.

**These are genuine artifacts, not written for this repository.** They are
otherwise unmodified except for one normalisation: project names and ticket
identifiers were replaced with neutral equivalents, because the project names
are themselves drawn from the third party's setting. No other text was
changed at publication, and nothing was redacted within a published file.

Two exceptions were made after publication, both to the same file and both
marked as such. The decision record on ticket lineage carries an annotation
appended on 2026-09-06 under ticket EM-006, under its own dated heading,
stating two defects in the scheme's lookup instructions that were found in
use; and a second appended on 2026-09-15 under ticket EM-023, stating two
further routes by which an identifier is spent that the first annotation's
command does not report. The original text above both annotations is
unchanged, and so is the earlier annotation: the second was added below a rule
of its own rather than by editing the first, because a dated annotation
records what was found on its date. EM-023 first made its correction by
editing the 2026-09-06 text in place; EM-023-001 restored that text and moved
the correction below, and both facts are stated in the second annotation.

They are annotations rather than supersessions because the decision is sound
and only its procedure was incomplete, and a reader copying the scheme needs
the correction beside it rather than in a file they may not open.

Where an artifact needed redaction to be publishable, it was **excluded rather
than redacted**. A partially redacted document invites the reader to
reconstruct what was removed, and a document with its substance removed is not
evidence of anything.

## Why publish the process at all

Because the process is mine and the ruleset is not.

The ticket lifecycle, the tier model, the no-shared-memory rule and the agent
policy were not derived from the domain. They would apply unchanged to any
project. Publishing them costs the rights-holder nothing, and it is the only
part of the work that transfers to anyone else.

## A note on the source project's own rules

The withheld project's agent policy contained these lines long before
publication was considered:

> Do not commit secrets, credentials, or the rules PDF. The PDF is gitignored;
> verify before staging.

> Do not paraphrase or quote large blocks of rule prose in code comments.
> Reference by section number. Full text belongs in the content files only.

The position in this document is not a decision made for publication. It is
the position the project was built under.
