---
id: EM-024-002
title: The gate count is restated away from its site, and it is not alone
status: ready
tier: standard
complexity: M
dependencies: [EM-024]
---

# EM-024-002 — The gate count is restated away from its site

## Context

EM-024 lands `docs/quality-gates.md`, "A count that describes the tree has one
site that goes red", which asks that a count describing the tree have exactly
one site, that every other mention name the site rather than the number, and
that in a repository with no suite the form asked for first is no number at
all. The round-1 independent review of EM-024 found the section's own commit
carrying the defect the section forbids, in the document the section lives in
and in a line that commit had just rewritten.

**The count of machine gates.** Its site is the code block at the top of
`docs/quality-gates.md`. The block holds four commands:
`sed -n '/^.\{3\}sh$/,/^.\{3\}$/p' docs/quality-gates.md | grep -c '^[a-z]'`
returns 4 at `b732abe`, the last commit that changes any document named in
Files below. The number four is restated away from that block at every one of
these sites, read from the sweep command in "The instrument" at the same
commit:

```
README.md:39:four machine checks
README.md:85:Four gates
docs/quality-gates.md:17:the other four
docs/quality-gates.md:18:four above
docs/tier-review-model.md:93:four machine checks
```

The enumeration is the count; no total is stated beside it, which is the
section applied to this ticket.

Two facts make this the ticket's headline rather than a tidy-up. It is
**OMN-024's exact shape** — the instance EM-024's Context leads with, where
one count lived in four places, a repair corrected one copy, and the round's
own repair re-created the claim it was repairing. And `README.md:39` was
**rewritten by the commit that added the rule**, `19cbb74`, whose diff is
`git diff 8abf61a..19cbb74 -- README.md`: the author of the rule edited the
line and did not see the count in it. That is the strongest available evidence
that the rule needed writing, and it is evidence against the option the
maintainer rejected, since the record was audited by its author and was wrong
anyway.

**The sweep.** EM-024's round-1 repair swept this repository mechanically for
the same class rather than repairing the sites it was handed. The class
question is: *which sentences in this repository's rule-bearing documents state
a number that counts something in this tree?* The sites below are the ones that
round judged in class, each by the section's own test — could the tree move so
that the number becomes wrong without anyone editing the sentence that states
it. None is asserted here to be wrong; under the section a number with no site
is a finding whether or not it is wrong, and measuring each is this ticket's
work.

- `docs/ai-contributor-policy.md:16` — "rather than searching five documents
  for it", in the map's own preamble. No site. The map table below it is not
  a list of five: `git ls-files 'docs/*.md' 'templates/*.md' README.md
  DISCLOSURE.md | grep -v 'docs/tickets/' | grep -v 'docs/adr/' | wc -l`
  returns 10 at `b732abe`. This is the sentence the new section's degraded-form
  paragraph names as its example of the repair — "searching the documents".
- `docs/ai-contributor-policy.md:332` — "If you cannot tick all seven", beside
  the §7 checklist that is its site. Adding a checklist item does not touch
  that line.
- `docs/ticket-lifecycle.md:188` — "Three things the scheme does not say for
  itself", beside the bolded paragraphs that follow it and are its site.
- `docs/tier-review-model.md:26` — "The two questions a review answers", in
  the index row for "What a review reports", which is the section that asks
  them. An index row restating a count of a list in another section of the
  same document is the shape twice over.
- `docs/tier-review-model.md:27` — "The three conditions", in the index row for
  "When review ends", same shape.
- `README.md:38` — "Three risk tiers", restating the tier table in
  `docs/tier-review-model.md`.
- `docs/tier-review-model.md:359` — "five of five, per the Review tables of the
  closed tickets". This one names its site in prose and states a baseline, and
  is the weakest of the set; it is listed because the number is still restated
  beside a site rather than derived from it.

`docs/adr/0003-every-rule-states-its-falsifier-and-a-control-can-be-retired.md`
carries "the five rule-bearing documents", which is the same shape. It is
**out of this ticket's population**: a decision record is a record of work and
not a document that states rules a contributor follows, so the map does not
govern it, and the new section asks for nothing retrospective. It is named
here so that a later reader knows it was seen and left.

**The instrument.** The sweep read each file with single line breaks treated as
spaces and matched a cardinal — spelled or in digits — followed within three
words by a plural noun or by "of", reporting the line each match starts on,
once per site. Written out, and run from the repository root:

```sh
cat > /tmp/wrapgrep.sh <<'SH'
pat="$1"; shift
for f in "$@"; do
  awk -v F="$f" -v P="$pat" '
    NR>1 { j = prev " " $0; s = 1
      while (match(substr(j, s), P)) { st = s + RSTART - 1
        if (st <= length(prev)) printf "%s:%d:%s\n", F, NR-1, substr(j, st, RLENGTH)
        s = st + (RLENGTH > 0 ? RLENGTH : 1) } }
    { prev = $0 }
    END { if (NR > 0) { j = prev; s = 1
      while (match(substr(j, s), P)) { st = s + RSTART - 1
        printf "%s:%d:%s\n", F, NR, substr(j, st, RLENGTH)
        s = st + (RLENGTH > 0 ? RLENGTH : 1) } } }' "$f"
done
SH
CARD='([Oo]ne|[Tt]wo|[Tt]hree|[Ff]our|[Ff]ive|[Ss]ix|[Ss]even|[Ee]ight|[Nn]ine|[Tt]en|[Ee]leven|[Tt]welve|[Tt]hirteen|[Ff]ourteen|[Ff]ifteen|[Ss]ixteen|[Ss]eventeen|[Ee]ighteen|[Nn]ineteen|[Tt]wenty|[Tt]hirty|[Ff]orty|[Ff]ifty|[0-9][0-9,]*)'
bash /tmp/wrapgrep.sh "(^|[^A-Za-z-])${CARD}( [a-z][a-z-]*){0,2} ([a-z][a-z-]*s([^A-Za-z-]|\$)|of )" \
  README.md DISCLOSURE.md docs/ai-contributor-policy.md docs/quality-gates.md \
  docs/tier-review-model.md docs/ticket-lifecycle.md docs/adr-process.md \
  templates/ADR.md templates/PR-DESCRIPTION.md templates/TICKET.md
```

Appending `| wc -l` to it emits 185 at `b732abe`, which is a candidate
population and not a finding count: most candidates are figures about
other projects with their baselines named, or stipulated constants, both of
which the section's scope paragraph puts out of reach.

**What the instrument does not catch, stated so the sweep is not read as
complete.** It reads one line joined with the next, so a phrase wrapped across
one line break is found and a phrase wrapped across two is not. It requires a
cardinal, so a count written as a word without one — "both", "each of the",
"a pair of" — is invisible to it, and so is a count spelled with a determiner
alone. It requires a plural noun or "of" within three words, which is why
`docs/ai-contributor-policy.md:332`, "tick all seven", is in the list above and
not in the instrument's output: it was found by reading the section, not by the
sweep. Its population is the rule-bearing documents named in the command and
no others; it does not read `docs/tickets/`, `docs/adr/`, `case-studies/` or `examples/`.
And it enumerates candidates only — the judgement of which candidate is a count
of this tree is a reader's, and this ticket's list is one round's reading of
it.

The wrap blindness is not incidental. The first version of this sweep missed
`docs/tier-review-model.md:93` entirely, because "the four" ends line 93 and
"machine checks" begins line 94; and EM-024-001's own locating command missed
its subject for the same reason. Both are instrument defects rather than
defects in the prose, and `docs/quality-gates.md` says so in "What this section
does not reach" rather than making a rule of it, because the second-instance
bar is not cleared by two instances in one round.

## Specification

Each site named in Context loses its restated number. The section's preferred
form for a repository of documents is the first thing to try at each: where the
record is a list, the list is the count and the reader derives it; where it is
a search, the sentence names the search. "The machine checks above", not "the
four machine checks". "Searching the documents", not "searching five
documents". "The conditions below", not "the three conditions".

Where a site cannot lose its number without losing something a reader needs at
that point, the number keeps exactly one site — the command that produces it,
written once with its baseline as §6 requires — and every other mention points
at that site. The executor states, per site, which of the two it chose and why;
"the number was needed here" is a claim a reviewer can test.

Three constraints on the repair:

- **`README.md:85` is a core-idea heading**, "Four gates are machine-checked;
  the fifth is countersigned where the work is." Removing the number changes
  what the heading says, and the fifth-gate contrast depends on it. If the
  count stays, the heading is the place to argue for it, and the argument goes
  in the description.
- **The map/index same-commit rule applies.** `README.md:38` and `:39` are
  index rows the contributor policy's "Keeping the map true" governs, and
  `docs/tier-review-model.md:26` and `:27` are that document's own index. A
  repair that changes what a row says about a section is checked against the
  section it names.
- **No rule is restated or re-scoped.** This ticket changes evidence and index
  prose, never an obligation. Any site where the number turns out to be load-
  bearing for a rule is left alone and recorded as such.

### Files

- `README.md` — the "Start here" rows and core idea 5
- `docs/quality-gates.md` — the paragraph above "The identical-script rule"
- `docs/tier-review-model.md` — the index rows, "The tiers", and the
  read-whole paragraph's evidence sentence
- `docs/ai-contributor-policy.md` — the map's preamble and §7's closing line
- `docs/ticket-lifecycle.md` — "Lineage", the sentence introducing the three
  bolded paragraphs

### Public surface

Every file listed is an instruction an adopter follows or an index into one.
Nothing an adopter must do changes; what changes is whether the numbers an
adopter reads can be checked.

### Behaviour

- After the change, the sweep command in Context, re-run at the closing commit,
  reports no site in the list above.
- The count of machine gates appears in the code block that is its site and
  nowhere else, or, where it stays, at one site whose keeping is argued.
- **This ticket adds no rule, so it states no falsifier.** The rule it applies
  is EM-024's, which carries its own.
- Where the repair changes an index row, the section that row names is read
  whole and the row is checked against it in the same commit, per "Keeping the
  map true".

## Acceptance criteria

1. AC1: the sweep command in Context, re-run at the closing commit and quoted
   with its output, reports none of the sites this ticket's Context lists,
   except any the description records as deliberately kept with its argument.
2. AC2: for each site, the description states which repair was taken — the
   number removed, or one site kept with its command — and why.
3. AC3: no rule text is changed. The diff shows edits to index rows, evidence
   sentences and prose only, and the description names the `##` section read
   whole for each document touched.
4. AC4: the instrument's own limits are restated in the description as they
   stand at close, since a later reader will use the AC1 command as evidence of
   cleanliness and needs to know what it cannot see.

## Out of scope

- `docs/tier-review-model.md`'s two "thirteen"s and the "eight" beside its own
  list. Those are EM-024-001's, which was raised first and folded the second
  "thirteen" in at EM-024's round-1 review.
- `README.md`'s two commit counts for one project. Those are EM-015's: they are
  figures about a private project's history that no command in this repository
  can produce, which is why they are a different repair.
- `docs/quality-gates.md`, "A count that describes the tree has one site that
  goes red", itself. If the rule is wrong, the finding belongs to EM-024.
- Decision records, tickets, case studies and examples. The map does not govern
  them and the section asks for nothing retrospective.
- Any figure about the control-plane project or the source project. Those carry
  their baselines and are §6's.

## References

- `docs/quality-gates.md`, "A count that describes the tree has one site that
  goes red" — the rule this applies
- `docs/ai-contributor-policy.md`, "Keeping the map true" — the same-commit
  rule the index repairs are checked against
- EM-024 — the ticket that landed the rule; its round-1 review is where these
  sites were found
- EM-024-001 — the sibling on the same class, in `docs/tier-review-model.md`
- EM-015 — the other count defect on this board, on figures no command here can
  produce

## Notes

Raised under the contributor policy's §4 at the round-1 independent review of
EM-024: found, not fixed in place. The reviewer's remedy for the gate count was
a sibling ticket and this is it; the sweep and the sites beyond the gate count
are the §6 class obligation discharged on that finding, and they are listed
here rather than repaired there for the same reason — the ticket EM-024 is the
rule, not the instances.

Proposed `standard`, matching EM-024-001: the change alters index prose and
evidence in documents an adopter follows and states no rule. The tier question
EM-007-002 owns applies here as to every documentation ticket on this board;
the executor may raise and never lower.

## PR Description

> Leave this section empty when authoring the ticket. The implementing
> agent fills it in before closing the ticket (move to `done/`).
