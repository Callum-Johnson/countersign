# Quality gates

What must pass before anything merges, at every tier.

```sh
ruff check .            # lint
ruff format --check .   # formatting, not negotiable, not hand-applied
mypy --strict           # strict type checking across all source packages
pytest --cov            # tests with coverage reporting
```

Contributors run these locally before opening a pull request. CI runs the
identical script afterwards. Failures block the merge regardless of tier.

There is a fifth gate that no tool runs. The falsification gate, below, is an
executor obligation discharged before the pull request is reported. It is
listed here because it is a condition of merge like the gates in the block
above, and because those cannot do its job.

**Retired when:** a gate is shown, over a stated count of pull requests, to
block merges that a reviewer passes without any change to the work — a
formatter fighting generated code, a type checker needing suppressions on most
files. That gate then costs review time and catches nothing; each gate below
carries its own line.

## The identical-script rule

The local command and the CI job are the same shell script in the repository,
not two configurations that resemble each other. Anything else produces the
"passes locally, fails in CI" conversation, which with an AI contributor
becomes an expensive loop: the agent cannot see CI, so it guesses, and it
guesses confidently.

**Retired when:** local and CI environments differ in a way one script cannot
express, and the "passes locally, fails in CI" loop is shown absent over a
stated population anyway.

**The script must not mutate state outside the working tree.** The ordinary
Python arrangement fails this: a gate script whose first step installs the
package in editable mode repoints the interpreter's import path at *this*
tree, for every process on the machine that shares that interpreter. With
several agents in parallel worktrees, one agent running the gate makes every
other agent's suite import the first agent's code. On the source project —
the rules engine in
[the growth case study](../case-studies/00-growth-2024-2026.md), which is
what "the source project" means throughout this document — three agents
independently deduced this and refused to run the script as written;
the gates were trustworthy only because each pinned its interpreter by hand
and printed the path as evidence. A script that is identical everywhere but
leaks across trees is identical in the wrong way. Install into an environment
the worktree owns, or run against the source tree without installing.

**Retired when:** the project runs one agent per machine by construction, so
that no process shares an interpreter with another tree.

## Review isolation

The identical-script rule's no-mutation constraint, one level up: a review
must not mutate the tree it reviews.

The falsification gate hands a reviewer a count to verify, and verifying it
looks like mutation — apply the wrong implementation, run the suite, count.
The gate is right to ask for that. Where it happens is the question. **Review,
including any mutation the gate asks for, runs in a worktree the reviewer
creates, owns and removes. The tree under review is read by the reviewer,
never written.** A review that writes nothing — a hosted reviewer reading a
diff — is not refused by this rule; what such a review cannot do is discharge
the run-the-suite duty, and that refusal is the tier model's. A reviewer that
must run the suite and cannot create a worktree — an agent handed a path and
nothing else — cannot discharge this rule; the review is then unavailable in
ADR-0002's sense, and the ticket says so rather than letting the review write
in place.

**The tree is checked after the review returns**, before any repair or further
round: the status command reports nothing untracked and nothing modified, and
the worktree list shows only the worktrees the executor created — a clone or a
copy elsewhere is not the tree under review and is not refused. Anything found
is a finding against the review, recorded as its own line after the round's
row in the record, outside the must-fix count and the columns, and removed
before the tree is used again, the closing commit included.

The mechanism this guards against, stated so the class is understood and not
only the file: an interpreter that imports a module of a fixed name at
start-up, from any directory on its path, will run whatever a file of that
name contains before the test runner or the type checker examines anything. A
copy that exits zero under those tools makes both gates pass having examined
nothing, and only a gate that reads files as text — lint — sees it. In CPython
the module is `sitecustomize`; which invocations reach a root-level copy
depends on the invocation, and the control-plane project's own record is the
authority on that. On OMN-021 on the control-plane project, one reviewer left
such a file at the root of the tree under review, in round 12 as that
project's policy-module comment records, and the lint gate was what failed;
another, in round 13, left a registered worktree the main tree's status
command does not show. The executor found both, by checking status and the
worktree list before every gate run as a private discipline. That discipline
is this rule.

It is the executor's check and not the reviewer's promise because the party
that will be blamed for a finding is the party that must be able to show the
tree was its own. A record that cannot say whether a finding was in the work
or in the review of it has lost the thing a review record is for.

**Retired when:** review is dispatched by a mechanism that cannot write to
the tree under review — a hosted reviewer with a read-only checkout and its
own environment — and the project has no other reviewer; the post-review
check then checks nothing, and the worktree rule constrains nobody.

## Coverage: no regression, not a threshold

There is no global coverage percentage to hit. The rule is **no regression on
files you changed**. If a file sat at 92% before your change and 89% after,
that blocks — restore it, or raise a follow-up ticket and justify the deferral
in the pull-request body.

A fixed threshold is easy to satisfy badly. A project at "80% minimum" with a
well-covered core and an untested periphery reports the same number as one
with the reverse, and a contributor adding untested code to an
already-well-covered file can stay above the line. Measuring the delta on
changed files asks the only question that matters: did *this change* come with
its tests?

**Retired when:** every change records a red count under the falsification
gate, over a stated population, at which point coverage adds nothing the count
does not say more precisely.

## Coverage measures execution, not discrimination

The rule above asks whether a change came with tests. It cannot ask whether
the tests would notice if the change were wrong. Coverage records that a line
ran; it does not record that any assertion depended on what the line did. A
test that executes a changed line and would pass under the old implementation
as well as the new one satisfies the coverage rule and pins nothing.

A fully covered file can be fully unpinned. On one ten-ticket wave of the
source project, four separate changes passed the no-regression rule, one of
them on a file at 100% of statements and branches, while shipping tests that
could not fail: reverting
the exact line each change had fixed left the whole suite green. The mechanism
was ordinary each time. A predicate ended in an inclusive comparison, so the
old and new implementations agreed at both values the tests used and differed
only in a band between them, and no test sat in the band. In another case two
readings of a specification coincided on every fixture in the repository,
which made them the same function as far as the suite could tell, so no single
test case could have separated them however carefully it was written.

No machine gate in this document catches that. Every instance was caught by
independent review, and only because a reviewer changed the code and counted.
The gate that follows moves the count to where it is cheapest: before the
report, by the executor.

*Not a rule.* This section describes what coverage measures; it carries no
falsifier because it constrains nothing.

## The falsification gate

For each behavioural claim a change makes, the executor:

1. **Names the counterfactual** — a plausible wrong implementation the change
   rules out. Not a syntax error; the neighbour a competent contributor could
   have written. The other side of an inclusive comparison. The other reading
   of the specification. The fix one branch too shallow.
2. **Applies it and runs the suite.**
3. **Records the count** of tests that go red, beside the claim, in the
   pull-request description's Falsification section.

**A count of zero means the test is decorative and the claim is unpinned.**
The change may still be correct. The suite cannot tell, and neither can a
reviewer reading it, and a zero written down is a fact a reviewer can act on
where a zero omitted is not.

Two cases the obvious arrangement does not cover:

- **No arrangement discriminates.** Some tests cannot be made to fail against
  any plausible wrong implementation: the change is a refactor, or the
  discriminating input does not exist in the fixture set. Keep the test, and
  **label it in its own docstring as non-discriminating**, naming what it
  would take. Deleting it loses a regression check still worth having. Leaving
  it unlabelled beside a real pin is how unpinned claims shipped in the first
  place: the label is what lets a reviewer tell the two apart.
- **More than one rival.** Two candidate readings that coincide on every
  existing fixture are indistinguishable to the suite, and one new case
  cannot separate three readings. The gate needs one discriminating case per
  rival, each with its own count.

The gate is an executor obligation, not a reviewer checklist item, and the
distinction is the point. On the source project every instance was found at
review, and each cost a full review round of rework. Putting the count in the
report means the reviewer verifies a number rather than derives one.

**Retired when:** over a stated population of changes every recorded red count
is non-zero and no reviewer's mutation has found an unpinned claim the
executor's count missed. The gate then costs a suite run per claim and catches
nothing review would not.

**A test pins a claim, not a mechanism.** A test that asserts a helper was
called, or that a case is absent from a list, defends the executor's belief
about how the code works, and turns red when the belief is corrected rather
than when a caller is let down. The assertion names what the change guarantees
to a caller; the docstring names the claim. The example, from OMN-021 on the
control-plane project, in the commit its round 11 records: a test asserting
that a directory name matched nothing on a list, with a comment explaining why
the absence was correct, on a list whose purpose was to match it — a test
written to defend a defect. Such a test passes the coverage rule and passes
this gate as stated, because the wrong implementation it rules out is real.
What it fails is the gate's purpose, which is that a red test means a claim
was violated. The gate's companion for the repair of a review finding — name
the class, falsify per sibling — is stated with the executor's other duties in
the contributor policy's §6 and not restated here.

**Retired when:** over a stated population of tests that predate this rule
or that review let through, those that assert a mechanism are shown to have
caught regressions that claim-level tests missed more often than they have
blocked a correct change to the mechanism.

**An exhaustive claim is derived, not listed.** A test that asserts something
of *every* member of a population derives that population from the thing it
describes; it does not restate it. A list the author wrote is a claim about
the tree wearing the costume of a check: the suite is green, the recorded red
count is non-zero, and the property the test names is absent, because the
rival reddens the members the list happens to hold. The gate above does not
reach this — it asks what a wrong implementation would redden, and here one
does. Three ways to satisfy it, in order of preference, because the first is
not always available:

1. **Assert at the convergence point.** Where every member must pass through
   one place, check there. A population that cannot be enumerated wrongly
   beats one enumerated carefully.
2. **Derive the population.** Walk the tree, read the registry, ask the
   module. Do not list the files, the call shapes or the spellings.
3. **Where neither is possible, the docstring says what the check cannot
   see**, and that statement is itself pinned — the shape this gate already
   uses for a non-discriminating test. Stating a gap honestly is a real
   answer; a gap left to the reader is not.

**A rival must redden a path a caller can take.** A count earned only through
an entry point no caller reaches is a zero wearing a number. The gate's
sentence above — a zero written down is a fact a reviewer can act on — does
not reach it, because nothing was written down as zero. Where the rival is
applied, the case that reddens names the caller that gets there.

This binds checks written after it. Nothing sweeps an existing corpus for
lists.

**Retired when:** over a stated population of reviews, a check written under
this rule is found to have derived its population and still missed a member —
the rule would then be asking for the wrong thing rather than for more care.
Or no reviewer finds a written-down population over a stated population of
changes, at which point the rule restates practice and leaves.

## A number determined elsewhere has one site that goes red

A number that something other than its own sentence determines is a claim in
exactly the sense the gate above uses: how many sites a search matches, how
many callers a function has, how many tests are Windows-only, how many entries
a list holds. Written into a sentence it is a copy of something the tree
already decides, and an unpinned claim. What it copies moves, the sentence does
not, and nothing goes red — prose that says seven where the tree holds nine
reads exactly like prose that is right. The rule sits with the gate because a
number with a site that goes red is a pinned claim, and the paragraph above is
what pinning means.

**Such a number has exactly one site, and that site is one that goes red when
what it counts moves.** Where the project has a suite, that site is a test that
measures the number, and prose that needs it names the test rather than
restating it. The test going red is the falsifier the sentence never had. Where
no such site is available the number is not written at all, which is the
paragraph on projects without a suite, below. The rule is one site, and a site
that fails; a test is how a project with a suite supplies them, and not the
rule itself.

**Which numbers this reaches. Ask what determines the number, not what it
counts.** Is there anything other than this sentence that fixes it — a list, a
table, a directory, a set of files, a command over the tree, another sentence
that decides it? If there is, the number is a copy of that thing and this
section reaches it. If there is not, the sentence is where the number is
decided, changing the number means editing that sentence, and this section is
done with it.

The question is settled by exhibiting the determiner, not by judging what the
number is about. A writer who says a number is in scope names its determiner; a
writer who says it is out names the sentence that sets it. Both are claims a
reader can put to the test by looking. Neither is what this section asked
before — could the tree move so that the number becomes wrong without anyone
editing the sentence — which no reader can check, and which could not separate
a stipulated constant from a restatement of one.

Worked, on this repository's own sentences. "The three conditions", in an index
row naming the section that lists them: the list determines it, so it is a
copy. "The two columns", written in this document and in the pull-request
template, where `docs/tier-review-model.md`, "What a review reports", is what
states them: also a copy, and the same shape as the first — which the previous
test could not say, because one looked like a count of a list and the other
like a constant. "A ticket takes at most three review rounds": nothing fixes
that but the sentence that sets it, so the sentence is its site. "Fifty is a
default, named as one": the same. A date, a version, a duration and an
identifier are the same again — the sentence that records them is where they
come from.

That is a narrowing and a widening at once, and both are stated here rather
than left in a diff. **Widened:** a stipulated constant restated away from the
sentence that sets it is now in scope, where the previous test put every
constant out of reach — a cap repeated in a second document is a copy like any
other, and drifts like one. **Narrowed:** a number whose determiner is not in
this tree — a figure about another project's history — has no site here, so its
own sentence is its site and the contributor policy's §6 binds it as it binds
every measured number: say how it was obtained. **Which tree is meant** is the
repository the change is being made in, at the commit under review, and nothing
wider; a number about someone else's tree is §6's and not this section's.

**One site, and every other mention names the site rather than the number.** A
rule that says only "measure it" reproduces the defect it repairs: a number
written in several places is corrected where the reader was looking and left
standing everywhere else. On the control-plane project's OMN-024 one count
lived in a description's member, in a later bullet of the same description, in
a test's docstring and in that test's failure message, and the round that
repaired it re-created the claim it was repairing. Under this section a number
found in a second place is a defect on its face, which a reader can see without
measuring anything: each copy is a determiner the other restates. Order does not
have to be established for that to hold — "first" says nothing useful about two
prose sentences each setting the same constant — so the defect stays decidable
whichever was written first, and what is open is only which copy becomes the
site. That is the writer's choice, and it is recorded where the number is kept.
What that clause costs where nothing goes red is stated below rather than left
implied.

**Where a number's determiner includes the sentence stating it, the instrument
excludes prose.** A number about a tree is usually a number about a tree that
also holds the documents describing it, and a text search cannot tell them
apart: the sentence claiming that no call to `GateRunner(` remains is itself a
line that a search for `GateRunner(` returns. Restricting the search to source
paths does not fix it, because the prose lives in the source as well — a
docstring is under `src/` too. An instrument that can settle such a claim reads
the tree as the language rather than as text: to a parser a docstring is a
string constant and never a call. OMN-024 established that over the rounds its
record carries. It is a property of the class and not of that ticket, so it is
stated here once, where the next reader of a claim of absence will meet it.

**An instrument that enumerates numbers may not require a noun after the
number.** A sweep for this class matches a number and then, usually, a plural
noun or "of", because that is what a count normally looks like written out. A
restatement does not look like that. By the time a number is being restated the
noun is already established, so the sentence reaches for the number alone —
"the other four", "the three that follow", "those eight", "beyond the four" —
and a pattern that demands the noun is blindest to precisely the form this
section exists to catch. That is measured rather than asserted: the sweep run
over this repository at the round-1 review of the ticket that added this
section missed sites of that form in this document, the one the section lives
in, and they were found only by a pattern written for a single count. An
instrument for this class
matches the number and stops. Reducing a candidate to a finding is the
determiner question above, which is a reader's to answer site by site and not a
pattern's to guess, and an enumeration claimed complete and actually short is
worse than one declared open with its coverage stated.

**What a reader does differently.** The contributor policy's §6 already binds
the writer, and a writer bound by it was wrong in every instance the ticket
that added this section names in its Context, all of them on one day, on one
project. None was found by a gate; the ones that were found at all were found
because a reviewer or an executor chose to re-measure something the record
asserted. This section changes what finding one costs. A reader meeting a
number asks what determines it, and **a number whose determiner is not named is
a finding whether or not the number is wrong** — the missing site is visible in
the sentence, where the wrongness is not. A reviewer who re-measures nothing
still finds these. That paragraph carries no count of the instances on purpose:
the list in the ticket is their one site, which is what this section asks.

**Where the project has no suite that can hold the test.** This repository is
such a project — it ships documents, and the numbers in them are determined by
ticket files, by lists and by other sections. The rule does not lapse and it
does not quietly become a promise. A command written into a document is a site,
but it is not a site that goes red: it runs when a reader chooses to run it,
and between one reading and the next nothing happens. So the form this section
asks for first, where nothing can fail, is the one with no number to defend.
**Where the determiner is a list, the list is the count and the reader derives
it; where it is a search, the sentence names the search.** Searching the
documents, not searching five of them. The conditions below, not the three
conditions.

**Where a number is written anyway, the exception is not the writer's to take
silently.** A number kept in prose, in a repository where nothing goes red,
keeps exactly one site — the command or the list that determines it, written
once with its baseline as §6 requires — and the change's description records,
at that site, **which determiner the number copies and why naming it does not
serve the reader there**. A number kept without that record is a defect on its
face, in the same way a second copy is, and visible in the same way: by
looking, without measuring. The form is the one §6 already uses for a repair
that names no class — the declaration is permitted, it is made in those terms,
and it is a claim the next reader can test. Without it the exception has no
test at all and swallows the rule, because every writer who keeps a number
believes it was needed.

**What the degraded form costs, said rather than implied.** For a number
written anyway, the one-site clause is enforceable only by a reader who looks:
nothing goes red, so a second copy is found by whoever happens to read both
places. That is the shape of the review obligation this section was chosen
over, reappearing on any project without a runner, and a section that admits
its form is weaker without admitting which weaker thing it becomes has not
admitted much. **It does not add that obligation.** No reviewer is asked to
reproduce the numbers a record asserts, and `docs/tier-review-model.md`, "What
a review reports", is untouched by this section. The answer to the degraded
case is the paragraphs above — write no number, and there is no second copy
for a reader to have to find; keep one and the argument is on the record where
a reader meets it.

**What this section does not reach.** A number something other than its
sentence determines, on the question stated above, and nothing else. Which
numbers are measured at all is settled by §6's measured-number bullet and is
not re-decided here. It is not a rule about duplicated prose: two sentences
that say the same thing are a matter of style until one of them is a number, at
which point they can disagree and only one is right. It says nothing about how
a number is found in a document beyond the paragraph on instruments above — a
phrase a search should have matched but missed because it wraps across a line
break is a defect in the searcher's instrument, not in this rule, and the
second-instance bar in `docs/tier-review-model.md` is not cleared for a rule
about it. And it asks for nothing retrospective — records written before it are
not audited under it.

**Retired when:** over fifty review rounds on a project that has adopted this
section, no round records a finding under it: no number found copying a
determiner it did not name, and none kept without the record the exception
above asks for. The population is findings recorded under this section and not
reproductions of the numbers a record asserts, which is what this section
counted before. Reproductions were observable in principle and inert in fact,
because nothing here asks anyone to reproduce a number, so that population
would never have accumulated, and a control that never accumulates a population
cannot be retired on evidence at all. Findings are already recorded — the tier
review model's per-round record carries them — so the count exists whether or
not anyone sets out to collect it, and a project that adopts this section and
finds nothing under it has what it needs to drop it. Fifty is a default, named
as one, and the population is named at all because the whole evidence for this
section is a single day, 2026-09-08, on a single project, in the instances the
ticket that added it names in its Context. The first adopting project's fifty
rounds replace the figure.

## Formatting is machine-applied

The formatter is authoritative and its output is not hand-adjusted. This is
worth stating explicitly in a repository with AI contributors, because an
agent asked to match surrounding style will otherwise produce a plausible
approximation of it, and review time gets spent on whitespace instead of
behaviour.

**Retired when:** the formatter's output is contested at review more often
than it is accepted, over a stated population of pull requests.

## Strict typing

Type hints are mandatory on every function signature, including private
functions and return types, and `--strict` must pass.

The value is sharpest with generated code. An agent that has misunderstood a
data shape produces code that reads fluently and fails the type checker
immediately. Without it the same misunderstanding survives review and surfaces
later as a runtime error in an unrelated place.

**Retired when:** the project's language or its generated code cannot satisfy
`--strict` without suppressions on most files, counted.

## Hooks may not be skipped

Skipping pre-commit hooks is on the forbidden-actions list. If a hook fails,
the cause gets fixed.

The rule exists because `--no-verify` is exactly the kind of locally
reasonable shortcut an agent will take to satisfy its immediate instruction,
and it defeats every gate above at once.

*Falsifier:* stated once, with the rule in the contributor policy's forbidden
actions, and not restated here.
