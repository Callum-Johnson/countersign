---
id: EM-024-002
title: The gate count is restated away from its site, and it is not alone
status: done
tier: standard
complexity: M
dependencies: [EM-024]
claimed_by: claude-opus-5
claimed_at: 2026-09-15
closed_at: 2026-09-15
---

# EM-024-002 — The gate count is restated away from its site

## Context

EM-024 lands `docs/quality-gates.md`, "A number determined elsewhere has one
site that goes red", which asks that a number something other than its own
sentence determines have exactly one site, that every other mention name the
site rather than the number, and that in a repository with no suite the form
asked for first is no number at all. The round-1 independent review of EM-024
found the section's own commit carrying the defect the section forbids, in the
document the section lives in and in a line that commit had just rewritten.

**Read this ticket at EM-024's round-3 redesign, not at its round-1 form.** The
section's scope test changed: it asked what a number counts, which no reader
could check, and it now asks what determines the number — a list, a table, a
directory, a command over the tree, another sentence that decides it. The site
list below was widened accordingly, and the sweep was rebuilt, because the
round-1 list was one round's *judgement* over a candidate population, and the
round-2 review found in-class sites it had missed. They are added below.

**The count of machine gates.** Its determiner, and so its one site, is the
code block at the top of `docs/quality-gates.md`:
`sed -n '/^.\{3\}sh$/,/^.\{3\}$/p' docs/quality-gates.md | grep -c '^[a-z]'`
returns 4 at `d470681`, the last commit that changes any document named in
Files below. The number is restated away from that block at every one of these
sites, read at the same commit from the wrap-tolerant matcher in "The
instrument" run with a pattern for this count alone —
`bash /tmp/wrapgrep.sh '[Ff]our (machine checks|gates|above)|the other four'`
over the same documents:

```
README.md:39:four machine checks
README.md:85:Four gates
docs/quality-gates.md:17:the other four
docs/quality-gates.md:18:four above
docs/quality-gates.md:303:the other four
docs/tier-review-model.md:93:four machine checks
```

`docs/quality-gates.md:303` is the redesigned section quoting "the other four"
as an example of the form a restatement takes, not a restatement of the gate
count, and it is a site for this ticket to leave alone. It is left in the
output rather than filtered out of it, because a sweep whose output has been
tidied is a sweep a reader cannot re-run. The enumeration is the count; no
total is stated beside it, which is the section applied to this ticket.

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
the same class rather than repairing the sites it was handed. Its class
question was *which sentences in this repository's rule-bearing documents state
a number that counts something in this tree?*, and answering it required a
judgement per candidate about what each number was about. The question is now
the one EM-024's round-3 redesign states: **for each number in these documents,
what other than its own sentence determines it?** A number with a determiner is
a copy and belongs to this ticket; a number its own sentence sets is that
sentence's own and is not. That question is answered by exhibiting the
determiner, which is why the list below names one per site.

None is asserted here to be wrong; under the section a number whose determiner
is not named is a finding whether or not the number is wrong, and settling each
is this ticket's work.

Line numbers below are read at `d470681`, the commit that lands the redesigned
section; the commands that produce them are in "The instrument".

Found by round 1 and unchanged in status:

- `docs/ai-contributor-policy.md:16` — "rather than searching five documents
  for it", in the map's own preamble. Determiner: the set of governed
  documents. The map table below it is not a list of five: `git ls-files
  'docs/*.md' 'templates/*.md' README.md DISCLOSURE.md | grep -v
  'docs/tickets/' | grep -v 'docs/adr/' | wc -l` returns 10 at `d470681`. This
  is the sentence the section's degraded-form paragraph names as its example of
  the repair — "searching the documents".
- `docs/ai-contributor-policy.md:335` — "If you cannot tick all seven".
  Determiner: the §7 checklist beside it. Adding a checklist item does not
  touch that line.
- `docs/ticket-lifecycle.md:188` — "Three things the scheme does not say for
  itself". Determiner: the bolded paragraphs that follow it.
- `docs/tier-review-model.md:26` — "The two questions a review answers", in the
  index row for "What a review reports". Determiner: that section. An index row
  restating a count of a list in another section of the same document is the
  shape twice over.
- `docs/tier-review-model.md:27` — "The three conditions", in the index row for
  "When review ends". Determiner: that section's numbered list.
- `README.md:38` — "Three risk tiers". Determiner: the tier table in
  `docs/tier-review-model.md`.
- `docs/tier-review-model.md:359` — "five of five, per the Review tables of the
  closed tickets". Determiner: those Review tables, which the sentence names.
  It is the weakest of the set — it names its determiner in prose and states a
  baseline — and is listed because the number is still restated beside its
  determiner rather than derived from it.

**Added at EM-024's round-2 review, and the reason they were missed.** Round 2
found in-class sites this list did not carry, some in files this ticket did not
name. They are not a longer tail of the same kind. Each bullet says which of
two failures let it through — the instrument could not see it, or the
instrument saw it and the judgement step dropped it — and that split is the
evidence for the redesign. It is measured by the commands in "The instrument"
below rather than counted here.

- `docs/adr-process.md:50` — "the three that follow show them applied".
  Determiner: the worked cases that follow in the same section. *Missed by the
  instrument: the cardinal is used as a pronoun.* This is a file the ticket did
  not previously name.
- `templates/TICKET.md:35` — "an adopting project may keep a fifth directory,
  `backlog/`, for such tickets beyond the four `docs/ticket-lifecycle.md`
  documents". Determiner: the directory scheme in `docs/ticket-lifecycle.md`.
  *Missed by the instrument: same form.* Also a file the ticket did not
  previously name, and the number is load-bearing for the fifth-directory
  contrast, so this is a candidate for the exception with its argument recorded
  rather than for removal.
- `docs/ai-contributor-policy.md:229` — "The last three are there because
  agents reliably over-engineer". Determiner: the closing bullets of §5.
  *Missed by the instrument: same form.*
- `docs/ai-contributor-policy.md:35` — "Those are the three ways to be wrong".
  Determiner: the ways enumerated in the sentence immediately above.
  *In the instrument's output and judged out of class* — the number looked like
  a figure of speech rather than a count of the tree, which is exactly the
  judgement the redesign removes.
- `docs/tier-review-model.md:493` — "Those eight are this rule's instances".
  Determiner: the list of ticket ids in the sentence before it. *In the
  instrument's output and judged out of class.* **Disposed of in EM-024-001,
  not here**, because it is a second restatement of the same "eight" that
  ticket already owns, in the same paragraph, and splitting one paragraph's two
  copies across two tickets is the duplication failure the section is about.

**Added at EM-024's round-2 review under the redesigned scope test.** These
were in the round-1 instrument's output and were judged out because they looked
like stipulated constants rather than counts of the tree. Under the question
"what determines this number?" they are copies like any other, and they are the
worked example the section now carries for why the old test could not tell the
two apart:

- `docs/quality-gates.md:79` — "outside the must-fix count and the two
  columns", in "Review isolation". Determiner: `docs/tier-review-model.md`,
  "What a review reports", which is where the columns are stated.
- `templates/PR-DESCRIPTION.md:90` — "each in one of the two columns the tier
  review model" defines. Same determiner.

`docs/adr/0003-every-rule-states-its-falsifier-and-a-control-can-be-retired.md`
carries "the five rule-bearing documents", which is the same shape. It is
**out of this ticket's population**: a decision record is a record of work and
not a document that states rules a contributor follows, so the map does not
govern it, and the section asks for nothing retrospective. It is named here so
that a later reader knows it was seen and left.

**The instrument, rebuilt at EM-024's round 3.** The round-1 sweep matched a
cardinal — spelled or in digits — *followed within three words by a plural noun
or by "of"*. That trailing requirement is what a count looks like when it is
first written. It is not what a restatement looks like: by then the noun is
established and the sentence says "the other four", "the three that follow",
"those eight". The pattern was therefore blindest to the form the ticket exists
to find, and the round-2 review found sites of exactly that form. The
requirement is dropped. **The sweep now matches a number and stops**, and the
work of deciding whether a candidate is a copy is the determiner question
above, asked site by site, which is a question with an exhibit rather than a
judgement.

Both patterns are given, because the difference between them is the measurement
that justifies the change. The matcher reads each file with single line breaks
treated as spaces, reporting the line each match starts on. Written out, and
run from the repository root:

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
DOCS="README.md DISCLOSURE.md docs/ai-contributor-policy.md docs/quality-gates.md
docs/tier-review-model.md docs/ticket-lifecycle.md docs/adr-process.md
templates/ADR.md templates/PR-DESCRIPTION.md templates/TICKET.md"

# the sweep this ticket now runs: a number, and nothing required after it
bash /tmp/wrapgrep.sh "(^|[^A-Za-z-])${CARD}([^A-Za-z-]|\$)" $DOCS

# the round-1 sweep, kept so the difference can be measured
bash /tmp/wrapgrep.sh "(^|[^A-Za-z-])${CARD}( [a-z][a-z-]*){0,2} ([a-z][a-z-]*s([^A-Za-z-]|\$)|of )" $DOCS
```

Appending `| wc -l` to each emits, at `d470681`, the last commit that changes
any of the ten documents named in `DOCS`: **575** for the sweep this ticket now
runs and **187** for the round-1 sweep it replaces. Both are candidate
populations and neither is a finding count. The broad figure is large because
"one" is an article in English far more often than it is a count, and because
every date, identifier and version in these documents is a number; the
determiner question is what reduces a candidate to a finding, and it is the
reader's to ask per site.

**What the instrument does not catch, stated so the sweep is not read as
complete.** It reads one line joined with the next, so a phrase wrapped across
one line break is found and one wrapped across two is not. It requires a
number, so a count written without one — "both", "each of the", "a pair of" —
is invisible to it. Its population is the ten documents named in `DOCS` and no
others; it does not read `docs/tickets/`, `docs/adr/`, `case-studies/` or
`examples/`. **This enumeration is open, not complete**, and a run of the AC1
command that reports nothing is evidence about the sites this ticket lists and
about nothing else.

**Why the round-1 sweep missed what it missed, measured rather than asserted.**
The sites round 2 added split two ways against the round-1 pattern, and
the split is read from its output — `bash /tmp/wrapgrep.sh "<round-1 pattern>"
$DOCS | grep -c '^<file>:<line>:'` at `d470681`, per site. It returns 0 for
`docs/adr-process.md:50`, `docs/ai-contributor-policy.md:229` and
`templates/TICKET.md:35`: the pattern could not see them, because the cardinal
is used as a pronoun. It returns 1 for `docs/ai-contributor-policy.md:35` and
for `docs/tier-review-model.md:493`: the pattern saw them and the judgement
step dropped them. The same command returns 1 for `docs/quality-gates.md:79`
and 2 for `templates/PR-DESCRIPTION.md:90`, the "two columns" sites, which were
also seen and dropped. So the instrument accounts for some of the loss and the
judgement for the rest — which is why EM-024's round-3 redesign changed both
and not only the pattern.

The same command run with the sweep this ticket now uses returns a non-zero
count for every site in both groups, and also for `docs/quality-gates.md:17`
and `:18` and `docs/ai-contributor-policy.md:335`, which round 1 could reach
only with a pattern written for one count. The instrument's share of the loss
is closed. The judgement's share is closed by the determiner question, and that
is EM-024's change rather than this ticket's.

The wrap blindness is not incidental either. The first version of this sweep
missed `docs/tier-review-model.md:93` entirely, because "the four" ends line 93
and "machine checks" begins line 94; and EM-024-001's own locating command
missed its subject for the same reason. Both are instrument defects rather than
defects in the prose, and `docs/quality-gates.md` says so in "What this section
does not reach" rather than making a rule of it, because the second-instance
bar is not cleared by two instances in one round. What the section *does* now
say is the one thing this round has enough evidence for: an instrument for this
class matches the number and stops.

## Specification

Each site named in Context loses its restated number. The section's preferred
form for a repository of documents is the first thing to try at each: where the
record is a list, the list is the count and the reader derives it; where it is
a search, the sentence names the search. "The machine checks above", not "the
four machine checks". "Searching the documents", not "searching five
documents". "The conditions below", not "the three conditions".

Where a site cannot lose its number without losing something a reader needs at
that point, the number keeps exactly one site — the command or the list that
determines it, written once with its baseline as §6 requires — and every other
mention points at that site. The section now requires the argument rather than
permitting it: the description records, at that site, **which determiner the
number copies and why naming it would not serve the reader there**. A site kept
without that record is a defect on its face, and "the number was needed here"
with no reason attached is not the record.

Constraints on the repair:

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
- `docs/quality-gates.md` — the paragraph above "The identical-script rule",
  and "Review isolation"
- `docs/tier-review-model.md` — the index rows, "The tiers", and the
  read-whole paragraph's evidence sentence
- `docs/ai-contributor-policy.md` — the map's preamble, "Keeping the map true",
  §5's closing paragraph and §7's closing line
- `docs/ticket-lifecycle.md` — "Lineage", the sentence introducing the bolded
  paragraphs that follow it
- `docs/adr-process.md` — "When to write one", the sentence introducing the
  worked cases
- `templates/TICKET.md` — the Specification section's note on a fifth directory
- `templates/PR-DESCRIPTION.md` — the Review section's line on the columns

The last three name files this ticket did not list before EM-024's round-2
review. They are named here rather than left to a later sweep, because an
enumeration that is short and reads as complete is worse than one declared
open.

### Public surface

Every file listed is an instruction an adopter follows or an index into one.
Nothing an adopter must do changes; what changes is whether the numbers an
adopter reads can be checked.

### Behaviour

- After the change, every site in the list above either states no number or
  states one whose determiner and whose argument for keeping it are on the
  record. Re-running the sweep is how the sites are re-located; it is not what
  shows the work is done, because the sweep enumerates candidates and not
  findings.
- The count of machine gates appears in the code block that determines it and
  nowhere else, or, where it stays, at one site whose keeping is argued.
- **This ticket adds no rule, so it states no falsifier.** The rule it applies
  is EM-024's, which carries its own.
- Where the repair changes an index row, the section that row names is read
  whole and the row is checked against it in the same commit, per "Keeping the
  map true".

## Acceptance criteria

1. AC1: every site this ticket's Context lists is disposed of, and the
   description says how, one line each: the number removed, or kept at one site
   with the determiner it copies and the argument for keeping it, or left alone
   with the reason. The sweep in Context is re-run at the closing commit and
   quoted with its output, **as the means of re-locating the sites and not as a
   clean bill** — the sweep enumerates candidates, its population is the ten
   documents it names, and the description says so at the point where it quotes
   the output, so that a later reader does not read an empty result as an
   absence of defects.
2. AC2: for each site, the description states which repair was taken — the
   number removed, or one site kept with its determiner — and why.
3. AC3: no rule text is changed. The diff shows edits to index rows, evidence
   sentences and prose only, and the description names the `##` section read
   whole for each document touched.
4. AC4: the instrument's own limits are restated in the description as they
   stand at close, since a later reader will use the AC1 command as evidence of
   cleanliness and needs to know what it cannot see. The description says in
   terms that the enumeration is open, and names the population the sweep reads.

## Out of scope

- `docs/tier-review-model.md`'s "thirteen"s and its restatements of the "eight"
  beside its own list, at `:490` and `:493`. Those are EM-024-001's, which was
  raised first, folded the second "thirteen" in at EM-024's round-1 review and
  the second "eight" in at its round-2 review.
- `README.md`'s two commit counts for one project. Those are EM-015's: they are
  figures about a private project's history that no command in this repository
  can produce, which is why they are a different repair.
- `docs/quality-gates.md`, "A number determined elsewhere has one site that
  goes red", itself, including the numbers it quotes as examples of the form it
  rejects. If the rule is wrong, the finding belongs to EM-024.
- Decision records, tickets, case studies and examples. The map does not govern
  them and the section asks for nothing retrospective.
- Any figure about the control-plane project or the source project. Those carry
  their baselines and are §6's.

## References

- `docs/quality-gates.md`, "A number determined elsewhere has one site that
  goes red" — the rule this applies
- `docs/ai-contributor-policy.md`, "Keeping the map true" — the same-commit
  rule the index repairs are checked against
- EM-024 — the ticket that landed the rule; its round-1 and round-2 reviews are
  where these sites were found
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

**Widened at EM-024's round-2 review and round-3 redesign**, again under §4 and
again found rather than fixed: the sites round 2 named, the two "two columns"
sites the redesigned scope test brings in, three files this ticket did not
list, the rebuilt instrument, and the acceptance criterion that stops a clean
sweep from reading as a clean bill. Nothing here was repaired in EM-024's tree;
EM-024 lands the rule and this ticket is still the instances.

Proposed `standard`, matching EM-024-001: the change alters index prose and
evidence in documents an adopter follows and states no rule. The tier question
EM-007-002 owns applies here as to every documentation ticket on this board;
the executor may raise and never lower.

## PR Description

### Ticket
EM-024-002 — The gate count is restated away from its site, and it is not
alone.

### Tier
`standard`, on one independent review pass. Every file touched is a process
document under `docs/` or `templates/`, or `README.md`, which the contributor
policy's map names; "The operative test" fixes the tier there. The pass ran
against a16ea73 and is row 1 of the Review table.

**On the dependency.** The frontmatter names EM-024, which is `in-progress`.
The rule this ticket applies — `docs/quality-gates.md`, "A number determined
elsewhere has one site that goes red" — landed on the default branch at
d669ead under the maintainer's direction to split EM-024: land the rule, leave
the ticket open for its record defects and its siblings. The dependency is on
the rule and the rule is in force.

### Summary
A number that something other than its own sentence determines is a copy. The
gate count is determined by the code block at the top of
`docs/quality-gates.md` and was restated away from it; the rest of the sweep's
sites are index rows, map preambles, checklist closers and prose restating a
number that a list, table, block or directory scheme determines. Every site the
ticket's Context names is disposed of below.

### Acceptance criteria
- [x] AC1 and AC2: every site the Context lists is disposed of, one line each,
  with the repair taken and why. The table is the enumeration; **no total is
  stated beside it**, which is this section applied to this ticket, and a
  reader who wants a count derives it from the rows.

  | Context site | Repair taken, and why |
  |---|---|
  | `README.md:39` "four machine checks" | Number removed. An index row describes what a section covers; the count added nothing the row needed and the block determines it. |
  | `README.md:85` "Four gates" | Rewritten to keep the claim and drop the number: "The gates a tool runs are machine-checked; the falsification gate is countersigned where the work is." The ticket's Constraints named this site as the one place the count could stay with an argument; it is not kept, because naming the gate carries the fifth-gate contrast without a number and without leaving an ordinal to count from. |
  | `docs/quality-gates.md:17` "the other four" | Number removed; the sentence names the site — "a condition of merge like the gates in the block above". |
  | `docs/quality-gates.md:18` "the four above" | Number removed; "those" resolves to the block named in the clause before it. |
  | `docs/quality-gates.md:303` "the other four" | **Left alone**, as the ticket directs. It is the section's own worked example of the form a restatement takes, not a restatement of the gate count. Now `:308`. |
  | `docs/tier-review-model.md:93` "four machine checks" | Number removed; "no tier that skips the machine checks" carries the obligation unchanged. |
  | `docs/ai-contributor-policy.md:16` "searching five documents" | Number removed — "searching the documents for it", which is the repair the section's own degraded-form paragraph names as its example. |
  | `docs/ai-contributor-policy.md:335` "tick all seven" | Number removed — "tick every item above", which resolves to the checklist directly above it and survives an item being added. |
  | `docs/ticket-lifecycle.md:188` "Three things" | Number removed, plural head kept: "The things the scheme does not say for itself, each found in use". |
  | `docs/tier-review-model.md:26` "The two questions" | Number removed from the index row; the section it names states them. |
  | `docs/tier-review-model.md:27` "The three conditions" | Number removed from the index row; same reason. |
  | `README.md:38` "Three risk tiers" | Number removed from the index row; the tier table determines it. |
  | `docs/tier-review-model.md:359` "five of five" | **Kept** — the one site. See the exception recorded below. |
  | `docs/adr-process.md:50` "the three that follow" | Number removed — "the cases that follow show them applied". |
  | `templates/TICKET.md:35` "a fifth directory … beyond the four" | Both numbers removed — "a further directory, `backlog/`, for such tickets, beyond the ones `docs/ticket-lifecycle.md` names". The additional-to-the-scheme contrast is what "a fifth" carried, and "a further" carries it without deriving from a count. |
  | `docs/ai-contributor-policy.md:229` "The last three are there" | Number removed and the boundary restored by naming the members: "The bullets on shims, flags and speculative abstractions". "Those closing bullets" was tried first and named no boundary a reader could derive. |
  | `docs/ai-contributor-policy.md:35` "the three ways to be wrong" | Number removed; the ways are enumerated in the clause immediately above. |
  | `docs/tier-review-model.md:493` "Those eight" | **Disposed of in EM-024-001**, at 77374a1, as the ticket directs — two copies of one count in one paragraph are repaired together. |
  | `docs/quality-gates.md:79` "the two columns" | Number removed; the finding still sits outside the must-fix count and outside the columns. |
  | `templates/PR-DESCRIPTION.md:90` "one of the two columns" | Number removed; the line already names `docs/tier-review-model.md` as what states them. |

  **The exception taken, with its argument.** `docs/tier-review-model.md`, now
  `:431`, keeps "five of five, per the Review tables of the closed tickets".
  The determiner it copies is those Review tables, at baseline 5d94db7, and
  both the determiner and the baseline are named in the same sentence, which
  is the one-site form §6 asks for. Naming the determiner without the number
  would not serve the reader there for a specific reason: EM-024-001, merged
  at b57e220, rewrote the Retired-when below it to say "The pre-rule rate is in
  the paragraph above, with its baseline and the records it was read from; it
  is not restated here". Removing the number would leave that falsifier
  pointing at a sentence that no longer carries a rate. It is one site because
  the only other copy was the one EM-024-001 removed.

  **The sweep, re-run at the closing commit.** The ticket's gate-count pattern,
  run with the wrap-tolerant matcher over the ten documents `DOCS` names:

      docs/quality-gates.md:308:the other four

  At d470681 the same pattern returned six rows. **This output is the means of
  re-locating the sites and not a clean bill**: it enumerates candidates over
  ten documents for one count, and the one row it returns is the site the
  ticket directs be left alone. The gate count read from its own site —
  `sed -n '/^.\{3\}sh$/,/^.\{3\}$/p' docs/quality-gates.md | grep -c '^[a-z]'`
  — returns 4 at the closing commit, unchanged.
- [x] AC3: no rule text is changed. The edits are index rows, evidence
  sentences and prose. Four edited lines sit inside normative paragraphs and
  each was checked: `docs/ai-contributor-policy.md` "Keeping the map true" —
  "the ways" is as closed a set as "the three ways"; §7's closing line —
  "every item above" reads on the checklist it closes and survives an item
  being added, where "all seven" did not; `docs/quality-gates.md` "Review
  isolation" — the finding still sits outside the must-fix count and outside
  both columns; `docs/tier-review-model.md` "The tiers" — gates mandatory at
  every tier, unchanged.

  The `##` section read whole before the repair, per "The repair is read
  whole", one per document touched: `README.md` — "Start here" and "The core
  ideas"; `docs/quality-gates.md` — the gate block and its following
  paragraphs, and "Review isolation"; `docs/tier-review-model.md` — the index
  table and "The tiers"; `docs/ai-contributor-policy.md` — "Which document
  settles what", "Keeping the map true", §5 and §7; `docs/ticket-lifecycle.md`
  — "Lineage"; `docs/adr-process.md` — "When to write one";
  `templates/TICKET.md` — "Specification"; `templates/PR-DESCRIPTION.md` — the
  Review section.
- [x] AC4: the instrument's limits, as they stand at close. **The enumeration
  is open.** The sweep's population is the ten documents named in its `DOCS`
  list and nothing else — no decision record, ticket, case study or example is
  read, and `DISCLOSURE.md` and `templates/ADR.md` are in the population but
  were not edited. The matcher reads each file with single line breaks treated
  as spaces and reports the line a match starts on, so a number split across a
  paragraph break is not seen. It matches a number and stops; deciding whether
  a candidate is a copy is the determiner question, asked site by site, which
  is a reader's judgement and not the pattern's. A candidate the reader judges
  out is invisible in the output, which is how two of the round-2 additions
  were missed at round 1. A later reader must not read an empty result as an
  absence of defects.

  One live instance of that openness, found by the round-1 reviewer and not in
  the Context list: `docs/tier-review-model.md:86` restates "the two columns"
  in a third document, away from its site. It is not a defect of this change
  and is recorded under Risks.

### Falsification
N/A for a behavioural claim — this repository publishes documents and runs no
suite. Per criterion, what a reader does differently: a reader who wants the
number of machine gates counts the block that runs them, and a reader who
edits that block does not leave five sentences elsewhere asserting the old
figure.

For each must-fix repaired, per the contributor policy's §6:

- R1.6 — class: **which repairs removed a claim along with a count?** The
  README core-idea heading is the instance. The question was asked of every
  sentence this branch rewrote rather than merely shortened. Siblings, each
  checked:
  - **`README.md` core idea 5** — the instance. "Four gates are
    machine-checked" asserted which gates a machine checks; the first
    replacement asserted the identical-script rule, which the body of the same
    paragraph already carries, and left "the fifth" counting from nothing.
    Repaired: the heading names the gates by what runs them and names the
    falsification gate rather than numbering it.
  - **`docs/ticket-lifecycle.md` "Lineage" intro** — same class, found by the
    same question and reported as R1.5: dropping "Three" took the plural head
    with it and left "each" quantifying over nothing. Repaired in the round.
  - **`docs/ai-contributor-policy.md` §5's closing sentence** — same class,
    reported as R1.7: "Those closing bullets" named no boundary a reader could
    derive. Repaired in the round by naming the bullets' subjects.
  - **`templates/TICKET.md`'s backlog sentence** — checked and sound. The
    reviewer confirmed the contrast survives: "beyond the four
    `docs/ticket-lifecycle.md` documents" used "documents" as a verb, and
    "beyond the ones `docs/ticket-lifecycle.md` names" keeps that reading while
    "a further directory" keeps what "a fifth" carried.
  - **Every index row and the two column sentences** — checked and sound. Each
    dropped a count from a noun phrase whose head survives, so no claim moved.
  What a reader does differently: a reader of core idea 5 still learns which
  gates a machine checks and which one is countersigned, instead of reading the
  identical-script rule twice and an ordinal with no antecedent.

- R1.2 — class: **which numbers did this change's own record state that
  something other than its sentence determines?** The previous commit's message
  is the instance: it asserted "sixteen restated counts" and "five places",
  both determined by the Context enumeration and the sweep, neither carrying a
  determiner, and "sixteen" does not reproduce — Context lists twenty sites, of
  which seventeen lose a number here. Siblings, each checked: this description
  states no total anywhere, the per-site table is the enumeration, and the
  Review row's counts are the round table's own field, which the template's
  countability rule governs. The commit message stands as written, because a
  record is not rewritten; 3a64ffe is where it is corrected.
  What a reader does differently: a reader auditing this ticket counts the
  table's rows rather than checking a total against them and finding it short.

- R1.1 — class: **which exception did this change take without recording it?**
  The kept site is the instance, and the only one: the description now names
  the site, the determiner it copies and the argument, under AC1 above. No
  other number is kept anywhere in the diff.

- R1.3 — note, and it is discharged by this description existing: the sweep is
  quoted with its output, each AC carries its evidence, the `##` sections read
  whole are named, and the instrument's limits are restated.
- R1.5 and R1.7 — notes, repaired in the round and recorded under R1.6's class
  above, since the class question found them.

### Routed, not repaired
R1.4 is routed. `docs/quality-gates.md:308` quotes "the other four", "the three
that follow", "those eight" and "beyond the four" as illustrations of the form
a restatement takes. After this branch and EM-024-001, none of the four
survives anywhere in the ten documents except in that example. The reviewer
judged, and I agree, that it is **not stale as a claim** — the phrases are
offered as shapes, not as pointers to live text, and the measured sentence
beside them is time-stamped to the round-1 review. What has thinned is its
force as an exhibit. The ticket's Out of scope reserves that section, including
"the numbers it quotes as examples of the form it rejects", so under the second
condition of "When review ends" it goes to the ticket that owns it: **EM-024**,
which is open in `active/` and owns that section. Nothing is owed unless EM-024
wants the example to keep pointing at live text.

### Out of scope (per ticket)
Confirmed; nothing exceeds it.
- `docs/tier-review-model.md`'s "thirteen"s and its "eight" restatements —
  EM-024-001's, and untouched here.
- `README.md`'s two commit counts — EM-015's, untouched.
- `docs/quality-gates.md`, the section itself — untouched; the whole of it is
  byte-identical apart from `:17`, `:18` and `:79`, which are outside it.
- Decision records, tickets, case studies and examples — untouched.
- Any figure about the control-plane or source project — untouched.

### How to verify
1. Re-run the gate sweep quoted under AC1 and compare with the output there.
2. `sed -n '/^.\{3\}sh$/,/^.\{3\}$/p' docs/quality-gates.md | grep -c '^[a-z]'`
   — 4, the count at its one site.
3. `git diff main...HEAD --name-only` — eight documents, exactly the eight in
   Files.
4. For any row of the AC1 table, open the file and check the sentence says what
   the row says it says.

### Risks / follow-ups
- **The enumeration is open, and one instance is already known.**
  `docs/tier-review-model.md:86` restates "the two columns" in a third
  document, away from the site that states them. The round-1 reviewer found it
  and correctly did not rank it a defect of this change, since it is not in the
  Context list. It belongs to the next sweep. Recorded here so it is not lost.
- **The sweep's blind spots are structural, not incidental.** The instrument
  cannot see a number split across a paragraph break, and cannot see a
  candidate a reader judged out. The second is how two round-2 additions were
  missed at round 1, and no change to the pattern fixes it — the determiner
  question is a reader's.
- `docs/quality-gates.md:308`'s example phrases are now archival, as R1.4
  records. A reader who goes looking for the live sites they were drawn from
  will not find them.

### Review
One independent review pass, per "The operative test" for a change to a
process document. No second pass is taken.

| Round | Must-fix | Where (rules / lists / documents / tests) | Inside previous round's fix | Repaired by |
|---|---|---|---|---|
| 1 | 3 (of 7 findings) | documents: the README core-idea heading lost its claim along with its count and left an ordinal counting from nothing, at the one site the ticket's Constraints named as the place to argue for keeping the number (must-fix, second column); the exception at the kept site was taken silently, with no determiner and no argument recorded (must-fix); the previous commit's own message restated two counts determined by the Context enumeration, one of which does not reproduce (must-fix); the four ACs' evidence did not yet exist at the reviewed commit; the section's own worked example now quotes four phrases with no live referent (routed to EM-024); "each" left quantifying over nothing in the lifecycle intro; the §5 closing sentence left no boundary a reader could derive | — | 3a64ffe |

Derived from the row and not asserted beside it: three must-fixes over one
review round, of which two are repaired here, one is discharged by this
description, and one further finding is routed. Round 1 has no round before
it, so its inside-previous-fix cell reads `—` and no line is uncountable.

- R1.6 · refuses · must-fix · the ticket's Constraints, "`README.md:85` is a core-idea heading … Removing the number changes what the heading says, and the fifth-gate contrast depends on it", and `docs/quality-gates.md`, "Where a site cannot lose its number without losing something a reader needs at that point" · the removal took the heading's claim with it and left "the fifth" with nothing in the heading to count from, at the exact site the ticket signposted — remedy: keep the claim and name the gate rather than numbering it; cost, if the remedy tightens a control: none, it loosens a repair; inside previous fix: —
- R1.1 · permits · must-fix · `docs/quality-gates.md`, "the change's description records, at that site, which determiner the number copies and why naming it does not serve the reader there. A number kept without that record is a defect on its face" · the one kept site was recorded as "one site is kept" and nothing more — remedy: name the site, the determiner and the argument; cost: none; inside previous fix: —
- R1.2 · permits · must-fix · `docs/quality-gates.md`, "a number found in a second place is a defect on its face", and the ticket's own Context, "The enumeration is the count; no total is stated beside it" · the previous commit's message asserted "sixteen restated counts" and "five places", determined by the Context enumeration and the sweep, and sixteen does not reproduce — remedy: drop both totals and let the per-site lines be the enumeration; cost: none; inside previous fix: —
- R1.3 · permits · note · `docs/ai-contributor-policy.md` §6, "Every acceptance criterion met and demonstrated in the pull-request description, with evidence" · none of the four ACs' evidence existed at the reviewed commit — remedy: the description at close; cost: none; inside previous fix: —
- R1.4 · permits · note · the ticket's Out of scope, "`docs/quality-gates.md` … including the numbers it quotes as examples of the form it rejects" · the section's worked example quotes four phrases whose live sites this branch removed, thinning it as an exhibit though not falsifying it — remedy: routed to EM-024, which owns that section; cost: none; inside previous fix: —
- R1.5 · permits · note · `docs/quality-gates.md`, "Where the determiner is a list, the list is the count and the reader derives it" · dropping "Three" took the plural head with it, leaving "each" quantifying over nothing — remedy: restore the head without the count; cost: none; inside previous fix: —
- R1.7 · refuses · note · the same rule · "Those closing bullets" named no boundary a reader could derive, so a checkable sentence became only a readable one — remedy: name the bullets by content; cost: none; inside previous fix: —

Both columns carry findings, and the second-column ones are the ones that
changed the repair: R1.6 is a removal that took a claim with it, ranked a
must-fix of the same rank as a first-column finding, and R1.7 is a repair that
left a sentence less checkable than it found it. Both are the failure mode
"What a review reports" names — a review that only ever tightens, or here a
repair that only ever deletes.

### Definition of Done (all tiers)
The four machine checks do not apply to a repository that publishes documents
and runs no suite; the falsification gate is discharged above, with N/A for the
behavioural claim and a class line per must-fix repaired. Every measured figure
names its baseline in the same sentence and is read from the command named
beside it. The independent pass a process-document change takes has run and is
recorded. The implementing
> agent fills it in before closing the ticket (move to `done/`).
