---
id: EM-022
title: Define ticket rationale, impact and unattended selection
status: ready
tier: critical
kind: governance
impact: multi-feature-blocking
delivery: enabling
why: "Without portable rationale and impact fields, an unattended scheduler cannot distinguish demonstrated blocking work from speculative work."
complexity: L
dependencies: []
claimed_by:
claimed_at:
blocked_at:
closed_at:
---

# EM-022 — Define ticket rationale, impact and unattended selection

## Context

Countersign defines a ticket's implementation contract and the assurance
required to merge it, but it does not define portable facts from which an
adopting project can choose *which* claimable ticket to work next. A project
therefore cannot delegate unattended selection deterministically while still
showing a maintainer why a ticket deserves capacity.

The missing distinction is not risk tier. `trivial`, `standard` and `critical`
answer how much assurance a change needs; they do not answer what harm follows
from deferring it. A small fix may leave a system unavailable, while a large
new feature may be an enhancement that can wait. The methodology needs a
separate impact scale, a concise causal rationale and a rule for automatic
selection that consumes declared facts rather than a model's reading of prose.

## Why this ticket should be worked

Without this change, a maintainer cannot inspect a ticket and reliably tell
whether it addresses an observed problem, unblocks a defined delivery slice or
adds speculative scope. An unattended scheduler either leaves work idle or
chooses by an arbitrary order, which can spend capacity on unneeded work while
degraded and blocking work remains.

Evidence: the existing template has `tier`, `phase` and `complexity`, but no
field that states deferred consequence, work kind or a concise causal reason;
the lifecycle has no automatic-selection rule. OMNISSIAH records the related
implementation prospect as `docs/suggestions/SUG-002-unattended-impact-ordered-ticket-scheduling.md`.

Deferring this change is acceptable only where a project selects every ticket
manually. It is not acceptable as the methodology's answer for a project that
authorises unattended ticket dispatch.

## Specification

### Files

- `templates/TICKET.md` — add required ticket metadata and a required causal
  justification section.
- `docs/ai-contributor-policy.md` — make the metadata and justification part
  of the ticket contract.
- `docs/ticket-lifecycle.md` — define selection among claimable tickets and
  the boundary between the portable rule and project-local authority.
- `docs/tier-review-model.md` — state that impact and delivery classification
  do not alter the risk tier or its review requirements.
- `templates/SCHEDULING-POLICY.md` — add a project-local policy template for
  unattended selection.
- `README.md` — keep the start-here map and core-idea summary true if the
  changed documents' scopes require it.

### Public surface

Every new ticket has these required frontmatter fields:

```yaml
kind: defect                 # defect | feature | maintenance | research | governance
impact: feature-blocking     # system-unavailable | multi-feature-blocking |
                             # feature-blocking | degraded | enhancement
delivery: slice              # slice | enabling | maintenance
why: "Without this work, <outcome> cannot <result>."
```

Every ticket also has a `## Why this ticket should be worked` section. It
names the affected outcome, the consequence of deferring the ticket, evidence
for that claim, and the condition under which deferral is acceptable. The
frontmatter `why` is a concise summary of that section, not a substitute for
it.

The impact values have this order, from greatest consequence of deferral to
least:

1. `system-unavailable` — a required build, test, deployment or runtime
   operation cannot proceed.
2. `multi-feature-blocking` — two or more defined delivery slices cannot
   proceed.
3. `feature-blocking` — one defined delivery slice cannot proceed.
4. `degraded` — an existing capability is impaired but remains usable or has
   a stated workaround.
5. `enhancement` — no existing committed capability is impaired.

`kind` classifies the work; `delivery` says whether it is an independently
demonstrable vertical slice, enabling work for a named slice, or maintenance.
Neither field, nor `impact`, changes the tier. The operative tier test remains
the sole rule for required review and assurance.

The lifecycle defines an optional unattended-selection rule for projects that
adopt a completed scheduling policy: choose only claimable tickets allowed by
that policy; order them by the declared impact scale; then apply the policy's
declared deterministic tie-breaker. The rule does not authorise dispatch,
review, merge, a tier reduction or a decision reserved to a human. A blocker,
policy refusal, gate failure or missing required approval stops the affected
ticket under the existing procedures.

The scheduling-policy template requires the maintainer to declare: eligible
impact values, concurrency limit, deterministic tie-breaker, stop and notify
conditions, and whether it authorises dispatch only or any later action. It
states that a project may not use it to bypass Countersign gates, independent
critical-tier review or any required human authorisation.

### Behaviour

- A ticket template makes `kind`, `impact`, `delivery`, `why`, and the causal
  justification section mandatory; a ticket with a field that does not use a
  declared value is not ready.
- A ticket's justification makes its impact auditable: it names an affected
  outcome, deferral consequence and evidence, rather than asserting an
  adjective such as "critical".
- A vertical slice is the thinnest independently demonstrable end-to-end
  outcome. Enabling or maintenance work may be horizontal, but names the
  slice or capability it enables where one exists.
- A project that has not adopted a completed scheduling policy continues to
  select work manually; this change does not create unattended authority.
- A project that has adopted one chooses unattended work only from claimable,
  policy-eligible tickets in declared impact order with a deterministic
  tie-breaker. An agent does not infer, upgrade or downgrade impact from the
  prose it reads.
- Impact, kind and delivery classification do not lower a ticket's tier,
  bypass any gate or weaken the review model.
- Every new rule introduced by this ticket states its falsifier in the
  adopted document.

## Acceptance criteria

1. AC1: the ticket template and contributor policy require all four metadata
   fields and the causal justification section, with each field's purpose and
   legal values stated in one authoritative location.
2. AC2: the lifecycle defines the five impact values, their ordering and the
   distinction between impact, kind, delivery and tier; the tier model states
   that impact cannot lower required assurance.
3. AC3: the template defines a vertical-slice classification and an enabling
   classification without requiring every ticket to be a vertical slice.
4. AC4: the scheduling-policy template requires eligible impacts, concurrency,
   deterministic tie-breaking, stop/notify conditions and action authority;
   it explicitly preserves gates, review and human-authorisation requirements.
5. AC5: the lifecycle permits automated selection only under an adopted
   project-local scheduling policy, and selection is from claimable,
   policy-eligible tickets by declared impact and then a deterministic
   tie-breaker.
6. AC6: the README map and any indexes affected by the new or changed governed
   documents are correct.
7. AC7: every new rule carries a `Retired when:` falsifier, and the PR
   description records a falsification result for every behavioural claim.

## Out of scope

- Implementing an unattended scheduler, ticket parser or merge authority in
  any adopting project, including OMNISSIAH.
- Authorising unattended dispatch or merge for any individual project.
- Reclassifying existing tickets or inventing their missing rationale.
- Changing the Countersign lifecycle states or the operative tier test.
- Defining product-specific meaning for a "critical feature" beyond the
  portable impact vocabulary above.

## References

- `docs/ai-contributor-policy.md` §§2, 3 and 6
- `docs/ticket-lifecycle.md`, "Claiming" and "Blocking"
- `docs/tier-review-model.md`, "The operative test" and "The tiers"
- `templates/TICKET.md`
- `docs/adr-process.md`, "Decisions about the process are themselves ADRs"
- OMNISSIAH `docs/suggestions/SUG-002-unattended-impact-ordered-ticket-scheduling.md`

## Notes

This changes contributor workflow and is therefore `critical` under the
process-surface clause. It adds rules under existing decisions rather than
changing the process's form, review authority or decision-record procedure;
the ticket record is the decision record described by `docs/adr-process.md`.

## PR Description

> Leave this section empty when authoring the ticket. The implementing agent
> fills it in before closing the ticket.
