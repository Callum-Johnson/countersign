---
id: EM-008
title: A decision reserved to another party is handled as ambiguity
status: ready
tier: critical
complexity: S
dependencies: []
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

> Leave this section empty when authoring the ticket.
