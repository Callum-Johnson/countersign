---
id: EM-008
title: A decision reserved to another party is handled as ambiguity
status: done
tier: critical
complexity: S
dependencies: []
claimed_by: claude-fable-5-1
claimed_at: 2026-09-06
closed_at: 2026-09-06
---

# EM-008 — A decision reserved to another party is ambiguity

## Context

`docs/ai-contributor-policy.md` §3 is the rule that ambiguity is escalated,
never resolved by invention: stop, write a `BLOCKER:`, move the ticket, pick
up something else. Its trigger word is "ambiguous", and it names the failure it
prevents — proceeding with a note in the pull request saying you assumed
something.

There is a second case with the same failure and a different trigger. Some
questions are perfectly clear and are simply not the executor's to answer,
because the project's own rules reserve them to another party. On a project
that adopts a governance surface — a class of change only the maintainer may
authorise — every question of the form "does this path belong on the surface"
is one. It is not ambiguous. It has two answers, both of them coherent, and
the rule that decides between them is that the executor does not decide.

The evidence is OMN-021 on the control-plane project that implements this
process mechanically. Over thirteen review rounds the executor accumulated ten
such questions into a child ticket, OMN-021-001, and continued working. That
child ticket's own text records that one of the ten, item 6, was closed by the
executor's diff during a generalisation in round 9 rather than asked, and was
reopened only because round 10's reviewer found three documents still calling
it open. Under §3 as written that is the forbidden case exactly: the diff
carried an answer to a question that was not the executor's, with a note. The
executor did not read §3 as applying, because nothing about the question was
unclear.

The cost of carrying a reserved question instead of blocking on it is specific
to how authorisation works. An authorisation names the hash of the exact diff
approved, and approval of one diff is not approval of a revised one. Every
round of work after the first reserved question is therefore work on a diff
whose shape the approver has not seen; if the approver's answer changes the
shape, the work between is discarded. On the source ticket the maintainer first
saw the shape after round 14, in a handover, with ten questions attached.

## Specification

Documentation changes only.

### Files

- `docs/ai-contributor-policy.md` §3 — a paragraph after the existing
  "specification is wrong rather than unclear" paragraph, stating the reserved
  case.
- `docs/ticket-lifecycle.md`, "Blocking" — one sentence naming the reserved
  case as a blocking trigger, so the operational form matches the policy.

### Public surface

N/A — this repository publishes documents. The change adds a trigger to an
existing rule and changes no rule's procedure.

### Behaviour

- §3 states that a question whose answer the project's rules reserve to a
  party other than the executor — a maintainer, an approver, a named owner —
  is handled by the same procedure as ambiguity: stop, state the question and
  the answers available, block. Clarity is not a defence; the test is who
  answers, not whether the executor could.
- §3 states that answering a reserved question provisionally in the diff,
  however reversible the provisional answer is, is the invention the section
  forbids. "One deletion undoes it" is a note saying you assumed something.
- §3 states the reason in terms of authorisation: work after the first
  reserved question is work on a diff the approver has not seen, and an
  approval of one diff is not an approval of a revised one. The first
  reserved question is therefore the point at which continuing costs the most
  and buys the least.
- §3 states that the first blocker carries every reserved question found by
  that point, so that the answering party sees them together, and that
  there is no threshold: one reserved question blocks.
- The lifecycle document's Blocking section names the reserved case in one
  sentence and defers to §3 for the rule.

## What this refuses, and what it costs

> Added 2026-09-05 on review of the wave, applying EM-010's two questions to the ticket that proposes them. A figure measured here names its baseline in the same sentence; a figure from a private project names the ticket section it is taken from; an assumption says so. Raised alongside EM-014; corrected after independent review of c0111ae.

**Refuses.**

- All work past the first reserved question, including work the answer
  cannot affect. The rule has no carve-out for unaffected parts, because the
  executor cannot reliably tell which parts are unaffected — that is the
  argument for the rule — but it is also a refusal of honest work. The
  ticket's Behaviour does not say so; this section does.
- Provisional answers that are cheap to reverse. "One deletion undoes it" is
  forbidden by name.

**Costs.**

- Throughput becomes the approver's response latency. On OMN-021, ten
  reserved questions accumulated over thirteen rounds, per OMN-021-001 as
  this ticket's Context cites it; under this rule the first would have
  blocked in whichever round it surfaced, which the record does not state,
  with the rest not yet discovered. Whether they surface in one further block
  or nine is not known. It is a question for a project that has a governance
  surface; this repository does not (Out of scope, first bullet), so it
  cannot be measured here. An assumption, stated as one: where the approver
  is one maintainer working evenings, one reserved question can cost a day.
- The cost this rule removes — work discarded when an answer changes the
  shape — is asserted from OMN-021's record, not measured by it. The record
  shows fourteen rounds and ten questions; it does not show how much of the
  work between would have been discarded. The saving is real in kind and
  unmeasured in size.

## Acceptance criteria

1. AC1: `docs/ai-contributor-policy.md` §3 states that a decision reserved to
   another party by the project's rules is handled by the blocking procedure,
   and that the test is who answers rather than whether the question is
   clear.
2. AC2: §3 states that a provisional answer carried in the diff, however
   reversible, is the invention the section forbids.
3. AC3: §3 states the authorisation reasoning — work after the first reserved
   question is on a diff the approver has not seen.
4. AC4: `docs/ticket-lifecycle.md` names the reserved case as a blocking
   trigger in one sentence without restating the rule.
5. AC5: Neither document defines what is reserved. That is each project's
   governance rule to state; this ticket only says what an executor does on
   meeting one.
6. AC6: Critical tier per ADR-0002: an independent agent that did not perform
   the work reviews this against the artifacts and records findings in the
   pull-request description.

## Out of scope

- Defining a governance surface for adopting projects. Countersign does not
  prescribe one; a project that has one names it in its own rules.
- The pacing rule for governance-surface tickets specifically — that such a
  ticket pauses after its first review round whether or not a reserved
  question has surfaced. That is a project-level rule and is raised on the
  source project as OMN-021-002.
- Any change to the false-block concern. A reserved question is a precise
  trigger because the project's rules name what is reserved; where a project
  has no such rule, §3's existing ambiguity test is unchanged.

## References

- `docs/ai-contributor-policy.md` §3 — the rule this ticket gives a second
  trigger.
- `docs/ticket-lifecycle.md`, "Blocking" — its operational form.
- OMN-021-001 on the control-plane project — the ten reserved questions, and
  its item 6, which records the closed-without-asking case in its own words.

## Notes

**Why this is not already covered.** A reader may say §3's "do not pick the
reading that makes the ticket easiest" already covers it. It does not, because
on the source ticket the executor did not pick the easy reading; it picked the
stricter one, and recorded that the maintainer could undo it. The failure was
not laziness, it was deciding at all.

**Working this with EM-007 and EM-009 to EM-011.** See EM-007's Notes: five
separable tickets from one body of evidence, workable as one wave.

## PR Description

### Ticket
EM-008 — A decision reserved to another party is ambiguity

### Tier
`critical` — process-surface change (clause 5): it adds a trigger to the
contributor policy's blocking rule.

**Independent review obtained**, per ADR-0002: a separate agent, given the
ticket, the diff and the two questions, and not the executor's reasoning,
reviewed the change in one rounds, read-only. Findings are under
Review; the tree was checked clean after each round.

### Summary
Policy §3 gains the reserved case as a paragraph after the
wrong-specification paragraph and before the non-convergence one: the test
is who answers, not whether the executor could; a provisional answer in
the diff is the invention the section forbids; the authorisation
reasoning; one reserved question blocks and the first blocker carries all
found by then; what is reserved is each project's rule to state. The
lifecycle's Blocking section names the case in one sentence and defers to
§3. The rule carries a Retired-when line, stated under ADR-0003's
exemption clause, which this description says so per that clause.

### Acceptance criteria
- [x] AC1: the reserved case handled by the blocking procedure, the test
  being who answers — `docs/ai-contributor-policy.md` §3, the paragraph
  beginning "A decision reserved to another party is handled the same
  way", "The test is who answers, not whether you could."
- [x] AC2: a provisional answer in the diff is the forbidden invention —
  same paragraph, "Answering it provisionally in the diff, however
  reversible the answer, is the invention this section forbids".
- [x] AC3: the authorisation reasoning — same paragraph, "an approval
  names the exact diff approved, and approval of one diff is not approval
  of a revised one".
- [x] AC4: the lifecycle names the case in one sentence without restating
  — `docs/ticket-lifecycle.md`, "Blocking", the last sentence of its second
  paragraph.
- [x] AC5: neither document defines what is reserved — the policy says
  "What is reserved is each project's own rule to state — this section
  says only what you do on meeting one"; the lifecycle says "the project's
  rules reserve".
- [x] AC6: independent review — see Review.

### Falsification
N/A — no behavioural claim. What a reader does differently, per criterion:
- AC1: an executor meeting a clear question the project reserves to
  someone else blocks instead of answering it, and does not argue that it
  was not ambiguous.
- AC2: an executor does not write "one deletion undoes it" in a diff.
- AC3: an executor stops at the first reserved question instead of
  carrying it through further rounds.
- AC4: a reader of the lifecycle's Blocking section learns the trigger
  exists and where the rule is.
- AC5: a project adopting these documents writes its own reserved list.

### Out of scope (per ticket)
Confirmed: no governance surface is defined; no pacing rule; the ambiguity
test is unchanged — the new paragraph is a second trigger for the same
procedure and does not touch the first. The ticket's Refuses section says
the rule refuses all work past the first reserved question with no
carve-out, including work the answer cannot affect; the landed paragraph
says that in its own words ("everything done after the first reserved
question is work on a diff the approver has not seen") and does not soften
it.

### Review
| Round | Must-fix | Where (rules / lists / documents / tests) | Inside previous round's fix | Repaired by |
|---|---|---|---|---|
| 1 | 0 (of 7 notes) | documents: the falsifier's second arm matchable by an adopter's initial state and carrying a scope statement; the total refusal implied rather than stated; "found by then" undefined; the BLOCKER form's "unclear" wording; one twenty-line paragraph; the first arm of the falsifier a counterfactual the record does not carry | — | the closing commit |

Derived total: 0 must-fix over one rounds.
Round 1, by column and rule:
- R1.1 · permits · the rule's Retired-when line · its second arm was
  matchable by a project's initial state and carried a scope sentence that
  belongs with the rule — remedy: the arm now needs a stated period under
  the policy, and the scope sentence is in the rule; no tightening. This
  repository reserves decisions in three places — lowering a tier to the
  reviewer, working a retirement ticket away from the refused executor,
  and a decision record's decision to the maintainer — so the arm is
  unmatched at landing.
- R1.2 · refuses · the reserved-case rule · the refusal of work the answer
  cannot affect was implied — remedy: stated, "including work you would
  judge unaffected".
- R1.3 · refuses · the same rule · "found by then" — remedy: "already
  found — several may surface in one reading of the ticket".
- R1.4 · refuses · §3's BLOCKER form · "what is unclear" fits ambiguity,
  not a reserved question — remedy: "or which question is reserved".
- R1.5 · refuses · §3 as a document · one twenty-line paragraph — remedy:
  broken before the reasoning.
- R1.6 · refuses · the falsifier's first arm · a counterfactual the record
  does not carry — recorded, not taken: the remedy is a tightening (one
  clause per reserved block naming the answer the executor would have
  taken), and the same form is already the falsifier of §3's first rule.
- R1.7 · the ADR-0003 duty · this description says the falsifier was
  stated under the exemption; done in Summary.
Post-review tree check after each round: `git status --porcelain` empty,
`git worktree list` showing only the main tree.

### How to verify
1. `grep -n "reserved" docs/ai-contributor-policy.md docs/ticket-lifecycle.md`
   — the rule once in §3, one sentence in Blocking.
2. `git diff f3a7b6c..HEAD --stat` — two documents and the ticket
   housekeeping; nothing else.
3. `wc -w` at f3a7b6c and at close: policy 1,970 to 2,269 and lifecycle 1,227 to 1,251 as the reviewer measured at 63be32b; §3 alone 174 to 473.

### Risks / follow-ups
- Throughput under this rule is the approver's latency, as the ticket's
  Costs section says. This repository has no reserved-decision rule of its
  own beyond what ADR-0002 and the tier model imply (who lowers a tier, who
  publishes); an executor here treating those as reserved would block on
  them, which EM-005's record shows has already happened once, before the
  rule existed.
- Whether one reserved question or nine surface per block is the question
  the ticket left to an adopting project; nothing here answers it.

