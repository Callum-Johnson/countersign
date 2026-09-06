# AI contributor policy

The rules AI coding agents work under. This is the document an agent is
required to read before its first edit in any session, and to re-skim on
return.

It exists because the failure modes of AI contributors are not the failure
modes of human ones. A human who does not understand a ticket asks. An agent
produces a confident, plausible, wrong implementation and a persuasive summary
of it. Most of what follows is designed to make that specific failure
expensive and visible rather than cheap and silent.

## Which document settles what

A map, so that a reader with a question goes to the place that settles it
rather than searching five documents for it. The table states no rule; each
row names where the rule is. What you must read before your first edit is
§7's checklist, not this table.

| Question | Where it is settled |
|---|---|
| What may I do, what may I not, and what do I do when I cannot proceed? | this document |
| How do I claim, block, batch and close work, and how are tickets numbered? | `docs/ticket-lifecycle.md` — the mechanics; §3 above states when to block |
| What must be true before I report this change done? | this document, §6 |
| What tier is my change, who reviews it, what does a review report, when does it end, and how does a rule leave? | `docs/tier-review-model.md` |
| Which machine checks must pass, what does the falsification gate ask of me, and where does a review run? | `docs/quality-gates.md` |
| Is this decision a record, and what does that record carry? | `docs/adr-process.md` |
| What shape does a ticket, a pull-request description or a decision record take? | `templates/` |
| What has this repository already decided, and on what reasoning? | `docs/adr/` |
| What is withheld from this repository, and why? | `DISCLOSURE.md` |

**Keeping the map true.** The map and the indexes it governs are wrong when
they name something that is not there, omit something that is, or send a
question to a place that no longer settles it. Those are the three ways to
be wrong, and each has a trigger.

This rule governs every document the map names, and any document added
under `docs/` or `templates/` that states rules a contributor follows. A
document that records work rather than states rules — a ticket, a decision
record, a case study — is not governed, which is why the rows name what
they do rather than everything in the repository. Where a row names a
directory, that row is what the rule keeps true, not one row per file
beneath it. Whether a new document states rules is the executor's judgement
and cannot be avoided: a rule that governed only what the map already names
could never catch a document the map is missing, which is the omission it
most needs to catch.

- A governed document added, removed or renamed updates the map, in the
  same commit.
- A change that moves where a question is settled — a rule leaving one
  document for another, a document's scope narrowing — updates the row that
  names it, in the same commit.
- A section added to, removed from or renamed in a governed document that
  carries an index updates that index, in the same commit. It updates the
  map only where it changes the question a row settles, which most section
  changes do not.

This is the directory/status invariant's argument applied to the documents:
two descriptions that must agree make drift visible at no cost, and a map
that has gone stale sends a reader to the wrong place with confidence.

**Retired when:** a review finds this map, or an index it governs, stale
more than once over a stated population of merged changes — the
same-commit rule is then not being followed, and a map nobody maintains
costs a reader more than navigating without one.

---

## 1. The no-shared-memory rule

Assume every other agent that has worked on this project, or will work on it
afterwards, has zero context from your session. They cannot see your chat
history, your scratchpad, your reasoning, or any note that does not live in
the repository.

This means:

- Anything you discover that a future contributor needs goes **into the
  repository** — a ticket, a code comment recording a non-obvious invariant,
  or a decision record if it is genuinely architectural.
- Never write "I" or "we" in a committed file. Address future readers
  directly.
- Never reference "the previous agent" or "the conversation" in tickets,
  commits or pull requests. If a decision was made, it is a decision record
  with its rationale, or it did not happen.

Almost every other rule in this document follows from this one.

**Retired when:** the project adopts a durable memory outside the repository
that every contributor reads before every session and that outlives the
sessions that wrote it. Until then the repository is the only such place, and
the rule protects the only record there is.

## 2. Scope is defined by the ticket

The ticket is the contract. It carries the specification, the acceptance
criteria, the references, and an explicit out-of-scope list.

- Implement what the ticket specifies. Nothing else.
- Anything on the out-of-scope list that you do anyway is grounds for
  rejection, however good the change.
- One ticket at a time per agent. Do not claim several in parallel.
- Do not start a ticket whose dependencies are unfinished.

**Retired when:** a project's closed tickets show out-of-scope work rejected
at review that the ticket's author, asked afterwards, would have accepted,
more often than they show scope creep caught — counted over a stated
population of tickets. The rule then costs more honest work than it stops.

## 3. Ambiguity is escalated, never resolved by invention

If anything in the ticket is ambiguous, **stop**. Add a comment to the ticket
file prefixed `BLOCKER:`, stating what is unclear — or which question is
reserved — and what you would need in order to proceed. Commit it, move the
ticket to the blocked state, and pick up something else.

Do not invent an interpretation. Do not pick the reading that makes the ticket
easiest. Do not proceed with a note in the pull request saying you assumed
something.

The same applies when the specification is wrong rather than unclear: raise a
`BLOCKER:` explaining what is wrong and what you would change. Do not
unilaterally rewrite the spec you were given.

A decision reserved to another party is handled the same way. Some questions
are perfectly clear and are simply not yours to answer, because the project's
rules reserve them to someone else — a maintainer, an approver, a named owner.
That is not ambiguity: the question has two coherent answers, and the rule
that decides between them is that you do not decide. The test is who answers,
not whether you could. Stop, state the question and the answers available, and
block. Answering it provisionally in the diff, however reversible the answer,
is the invention this section forbids; "one deletion undoes it" is a note
saying you assumed something.

The reason is how authorisation works: an approval names the exact diff
approved, and approval of one diff is not approval of a revised one, so
everything done after the first reserved question is work on a diff the
approver has not seen, and if the answer changes the shape, the work between
is discarded — including work you would judge unaffected, since which parts
are unaffected is the answer's to decide. The first reserved question is
therefore the point at which continuing costs the most and buys the least. The
first blocker carries every reserved question already found — several may
surface in one reading of the ticket — so that the answering party sees them
together; there is no threshold, and one reserved question blocks. What is
reserved is each project's own rule to state — this section says only what you
do on meeting one, and where a project reserves nothing, the ambiguity test
above is unchanged.

**Retired when:** over a stated population of blocks raised on reserved
questions, the answering party's answer never changed the shape of the diff
the executor would have produced, so that the discarded work the rule exists
to prevent was never going to be discarded; or, after a stated period under
this policy, the project has adopted no rule reserving any decision, so that
the trigger has had nothing to match.

Non-convergence is a further trigger: a critical-tier review that reaches the
round cap in `docs/tier-review-model.md`, "When review ends", blocks by this
same procedure, with its review record attached.

**Retired when:** blocked tickets on a project are, over a stated population,
routinely unblocked with the reading the executor would have taken. The block
then buys nothing the executor did not already know, and its cost is the
answering party's latency.

## 4. Discovered work becomes a ticket with recorded lineage

When you find something else that needs fixing, you do not fix it. You raise a
ticket for it, numbered as a child of the ticket you were working on, and
reference it from your pull request.

A ticket raised while working `PRJ-284` is `PRJ-284-001`. One raised while
working *that* is `PRJ-284-001-001`, without limit. Lineage records **where a
ticket came from, not what blocks it** — dependencies are stated separately
and may not include the parent.

Recording the discovery only in a pull request body, a report, or a summary
message is not acceptable. It must be a ticket file. Findings that live in
prose get lost; findings that live in the ticket directory get worked.

This also gives every unit of work a traceable origin, which matters when you
are trying to reconstruct why a change was made months later.

**Retired when:** child tickets raised under this rule are, over a stated
population, closed unworked as not wanted at a rate that shows the ticket file
is ceremony and a line in the pull-request body would have served. One in five
over the project's first fifty such tickets is the default rate, named as a
default.

## 5. Forbidden actions

Universal. They apply on every ticket whether or not the ticket restates them.

- **Do not skip pre-commit hooks.** If a hook fails, fix the cause.
  **Retired when:** the gate runs only in CI and no local hook exists, so there
  is nothing to skip. This is the one falsifier for this rule; the quality
  gates restate the rule and reference this line.
- **Do not amend or rewrite commits already pushed** to a shared branch.
  **Retired when:** the branch model makes every pushed branch single-author
  until merge, so no one else's history can be rewritten.
- **Do not force-push to the main branch** under any circumstances.
  **Retired when:** the project's history model changes such that the rule
  protects nothing — there is no observed failure that retires it; its
  falsifier is on the cost side.
- **Do not commit secrets, credentials, or licensed source material.**
  Verify before staging.
  **Retired when:** a pre-commit scanner blocks every commit containing key
  material or a listed term, and has done so on a stated population of
  commits; a later control then covers what this rule was added for.
- **Do not quote or paraphrase large blocks of third-party text** in code or
  comments. Reference by section identifier instead.
  **Retired when:** the project holds a licence to the third-party text that
  permits reproduction, at which point the rule protects nothing.
- **Do not add backwards-compatibility shims** for code written in the same
  session. If you change a signature, update the callers.
  **Retired when:** the project ships a signature to callers outside the
  repository within a session, so that updating the callers is not in the
  executor's power.
- **Do not add feature flags or environment toggles** unless the ticket asks
  for one.
  **Retired when:** the project's release process requires a flag on every
  change, so that every ticket asks and the rule is noise.
- **Do not write speculative abstractions** for hypothetical future needs.
  Three similar lines beat a premature interface.
  **Retired when:** a project's review record shows, over a stated population,
  that similar lines left unabstracted under this rule were later unified at
  a higher cost than an interface at the second occurrence would have been.

The last three are there because agents reliably over-engineer when uncertain.
Given an unclear requirement, an agent will produce an abstraction that covers
every reading of it. That is not caution — it is unreviewable code.

## 6. Definition of done

- Every acceptance criterion met and demonstrated in the pull-request
  description, with evidence.
- Tests added for new behaviour. Existing tests pass.
- Linter, formatter and strict type-checking all clean.
- Coverage on changed files has not regressed.
- The falsification gate is discharged: for each behavioural claim, the
  wrong implementation the change rules out is named, applied, and the count
  of tests that go red is recorded. A count of zero is reported as a zero,
  not omitted. The gate and its two special cases are in
  `docs/quality-gates.md`; this is a pre-report duty, not something review is
  expected to catch.
- A review finding is repaired at its class. For each finding repaired, the
  description names **the class** — the question which, asked of the whole
  change, produces this finding and its siblings: "what does the interpreter
  load" is a class, "`.py` files at the root" is an instance — and **the
  siblings** that question enumerates, each with the test that pins it and the
  count of tests that go red under its wrong implementation, one case per
  rival as the gate already requires. A repair that names no class says
  **repair of the instance**, in those words. That is permitted — some
  findings are singular — and it is a claim the reviewer can check: the next
  round finding a sibling is then a finding against the repair's own claim. A
  class with no finite enumeration — "what could a user type" — is recorded as
  the third condition of "When review ends" in `docs/tier-review-model.md`
  records a list: best-effort, with the coverage stated. Where the change has
  no suite, each sibling says what a reader would do differently, as the
  template says for a claim. The form is in `templates/PR-DESCRIPTION.md`, and
  the reason a test pins a claim rather than a mechanism is with the gate in
  `docs/quality-gates.md`.
  **Retired when:** over a stated population of critical-tier tickets, repairs
  declared "repair of the instance" draw a sibling finding in the next round
  no more often than repairs that named a class; the enumeration then costs a
  suite run per sibling and prevents nothing.
- Every measured number in the description names, **in the same sentence**,
  the baseline it was measured against: the commit, the branch, the date, or
  the population counted. A number without its baseline is indistinguishable
  from an inherited one once written down, and inherited numbers drift — they
  are restated, incremented and believed by readers who never had the source.
- **A measured number a command can produce is read from that command's
  output**, and the description names the command, once for a class of figures
  one run produces. This bullet reaches what the bullet above reaches, and a
  measured number is one the description asserts as a fact about a tree or its
  history — a count, a size, a date, a proportion — such that re-running the
  command would confirm it or refute it. A number that names something rather
  than measures it asserts no such fact and is outside this bullet: a ticket
  id, a section number, a finding number, an ordinal in a list. The test is
  whether a command could disagree with the number, not what kind of token it
  looks like. You do not count, and you do not estimate what a pending edit
  will change: run the command after the last commit that changes what it
  counts, and where the closing commit changes it — a note taken at close, a
  re-flow — run it again there. Where no command can produce the measurement,
  say how it was obtained, which is what makes an inherited figure visible as
  one. An agent asked for a count produces a plausible one, and a plausible
  count beside a correctly named baseline is the most expensive kind of wrong
  number: it survives every check the description carries. This is the
  falsification gate's demand applied to figures — a number nobody re-ran is
  unpinned, and naming its baseline makes it look pinned.
  **Retired when:** over a stated population of closed tickets, figures
  reported under this rule are found wrong as often as the figures reported
  before it; the rule then costs a command per class of figure and catches
  nothing.
- For critical-tier work, a second reviewer has approved.

The pull-request description is appended to the ticket file before the ticket
closes. It does not live only in a code-forge UI, because the repository has
to remain the record.

**Retired when:** any item in this list is shown, over a stated population of
closed tickets, to be satisfied nominally on every ticket without changing the
work — a Falsification section that reads N/A on every code change, a baseline
that is always the same commit. The falsification gate's own falsifier is
stated with the gate in `docs/quality-gates.md`.

## 7. Pre-flight checklist

Confirmed before the first edit of any session:

- [ ] I have read this document end to end, or skimmed it if returning.
- [ ] I have read my ticket in full, including acceptance criteria, and its
      Context, Files and Behaviour agree with one another; where they did
      not, I blocked under §3 before writing anything. This is the reading
      `docs/tier-review-model.md`, "When review ends", asks for after a
      repair, applied at claim.
- [ ] I have read the design sections my ticket references.
- [ ] I have read any external references the ticket cites.
- [ ] I have claimed the ticket by the documented procedure.
- [ ] I am on a branch whose name begins with my ticket identifier.
- [ ] I have confirmed my review tier using the operative test.

If you cannot tick all seven, do not write code yet.

**Retired when:** the transcript shows the ticks made without the reads — a
ticket blocked on a reference its executor had ticked as read — more than once
over a stated population. The checklist then produces the nominal satisfaction
it exists to prevent.

---

## Why a checklist rather than instructions

*Not a rule.* This section explains the one above and constrains nothing; it
carries no falsifier.

Instructions describe intent and are easy to satisfy nominally. A checklist
produces a verifiable claim: an agent that has not read the design sections
cannot honestly tick the box, and the tick is in the transcript.

It is the same reason the ticket status is stored both in a frontmatter field
and in the directory path. Redundant state that must agree is a cheap,
constant integrity check — the workflow cannot quietly drift without leaving a
contradiction behind.
