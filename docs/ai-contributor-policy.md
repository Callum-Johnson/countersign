# AI contributor policy

The rules AI coding agents work under. This is the document an agent is
required to read before its first edit in any session, and to re-skim on
return.

It exists because the failure modes of AI contributors are not the failure
modes of human ones. A human who does not understand a ticket asks. An agent
produces a confident, plausible, wrong implementation and a persuasive summary
of it. Most of what follows is designed to make that specific failure
expensive and visible rather than cheap and silent.

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

## 2. Scope is defined by the ticket

The ticket is the contract. It carries the specification, the acceptance
criteria, the references, and an explicit out-of-scope list.

- Implement what the ticket specifies. Nothing else.
- Anything on the out-of-scope list that you do anyway is grounds for
  rejection, however good the change.
- One ticket at a time per agent. Do not claim several in parallel.
- Do not start a ticket whose dependencies are unfinished.

## 3. Ambiguity is escalated, never resolved by invention

If anything in the ticket is ambiguous, **stop**. Add a comment to the ticket
file prefixed `BLOCKER:`, stating what is unclear and what you would need in
order to proceed. Commit it, move the ticket to the blocked state, and pick up
something else.

Do not invent an interpretation. Do not pick the reading that makes the ticket
easiest. Do not proceed with a note in the pull request saying you assumed
something.

The same applies when the specification is wrong rather than unclear: raise a
`BLOCKER:` explaining what is wrong and what you would change. Do not
unilaterally rewrite the spec you were given.

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

## 5. Forbidden actions

Universal. They apply on every ticket whether or not the ticket restates them.

- **Do not skip pre-commit hooks.** If a hook fails, fix the cause.
- **Do not amend or rewrite commits already pushed** to a shared branch.
- **Do not force-push to the main branch** under any circumstances.
- **Do not commit secrets, credentials, or licensed source material.**
  Verify before staging.
- **Do not quote or paraphrase large blocks of third-party text** in code or
  comments. Reference by section identifier instead.
- **Do not add backwards-compatibility shims** for code written in the same
  session. If you change a signature, update the callers.
- **Do not add feature flags or environment toggles** unless the ticket asks
  for one.
- **Do not write speculative abstractions** for hypothetical future needs.
  Three similar lines beat a premature interface.

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
- Every measured number in the description names, **in the same sentence**,
  the baseline it was measured against: the commit, the branch, the date, or
  the population counted. A number without its baseline is indistinguishable
  from an inherited one once written down, and inherited numbers drift — they
  are restated, incremented and believed by readers who never had the source.
- For critical-tier work, a second reviewer has approved.

The pull-request description is appended to the ticket file before the ticket
closes. It does not live only in a code-forge UI, because the repository has
to remain the record.

## 7. Pre-flight checklist

Confirmed before the first edit of any session:

- [ ] I have read this document end to end, or skimmed it if returning.
- [ ] I have read my ticket in full, including acceptance criteria.
- [ ] I have read the design sections my ticket references.
- [ ] I have read any external references the ticket cites.
- [ ] I have claimed the ticket by the documented procedure.
- [ ] I am on a branch whose name begins with my ticket identifier.
- [ ] I have confirmed my review tier using the operative test.

If you cannot tick all seven, do not write code yet.

---

## Why a checklist rather than instructions

Instructions describe intent and are easy to satisfy nominally. A checklist
produces a verifiable claim: an agent that has not read the design sections
cannot honestly tick the box, and the tick is in the transcript.

It is the same reason the ticket status is stored both in a frontmatter field
and in the directory path. Redundant state that must agree is a cheap,
constant integrity check — the workflow cannot quietly drift without leaving a
contradiction behind.
