---
id: EM-022
title: Define ticket rationale, impact and unattended selection
status: in-progress
tier: critical
kind: governance
impact: multi-feature-blocking
delivery: enabling
why: "Without portable rationale and impact fields, an unattended scheduler cannot distinguish demonstrated blocking work from speculative work."
complexity: L
dependencies: []
claimed_by: codex
claimed_at: 2026-09-07
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

### Resolved review-cap block

Three independent review rounds reached Countersign's review cap. Rounds one
through three found 5, 1 and 1 must-fixes respectively; the third repair is
`5fe7998`.

On 2026-09-07, the maintainer directed a fourth independent review of the
final evidence. This reopens the ticket solely for that review. It does not
authorise a scope change, merge, tier reduction or an exception to any other
gate.

### Resolved fourth-review evidence block

The authorised fourth review found that the persisted falsification command
checked fragments of compound claims. On 2026-09-07, the maintainer directed
that those claims be split into independently falsifiable claims. This reopens
the ticket solely to make that evidence repair. A fifth independent review
remains required before the ticket can close.

### Resolved fifth-review block

The split-claim repair is `12796ab` and its 17 independent mutations pass. On
2026-09-07, the maintainer directed the fifth independent review. This reopens
the ticket solely for that review; it does not authorise a scope change, merge,
tier reduction or an exception to any other gate.

BLOCKER: The fifth review found that the evidence, human-authority and
canonical-order mutants leave other wording that still establishes each named
guarantee. Either make each mutant falsify the guarantee as a whole or narrow
the table claims to the precise fragments tested, then obtain maintainer
direction for a sixth independent review before closing.

### Resolved sixth-review block

On 2026-09-07, the maintainer directed the final repair and sixth independent
review. The repair makes each disputed mutant remove every supporting statement
for its documented guarantee, and names only the documentary guarantees the
verifier can establish. This reopens the ticket solely for that work and
review; it does not authorise a scope change, merge, tier reduction or an
exception to any other gate.

## PR Description

### Ticket

EM-022 — Define ticket rationale, impact and unattended selection

### Tier

Critical. This changes the contributor workflow and the template every
adopting project uses.

### Summary

Tickets now distinguish risk tier from deferred impact, work kind and delivery
classification, and carry a concise `why` plus an evidence-bearing causal
justification. Countersign now defines an optional project-local policy for
impact-ordered unattended selection; it grants only the action that a
maintainer records and preserves every existing assurance boundary.

### Acceptance criteria

- [x] AC1: template and contributor policy require the metadata and causal
  justification — `templates/TICKET.md` and
  `docs/ai-contributor-policy.md`, §2.
- [x] AC2: lifecycle defines the impact scale and the tier model preserves
  assurance independence — `docs/ticket-lifecycle.md`, "Ticket rationale,
  impact and delivery", and `docs/tier-review-model.md`, "Impact does not
  set assurance".
- [x] AC3: the template defines `slice`, `enabling` and `maintenance` without
  requiring every ticket to be a slice — `templates/TICKET.md` before
  "Why this ticket should be worked".
- [x] AC4: the scheduling-policy template requires the authority and ordering
  facts — `templates/SCHEDULING-POLICY.md`.
- [x] AC5: unattended selection is limited to claimable, policy-eligible work
  by canonical impact order and deterministic tie-breaker —
  `docs/ticket-lifecycle.md`, "Unattended selection".
- [x] AC6: the README, policy map and ticket board describe the added
  lifecycle scope and both new tickets — `README.md`,
  `docs/ai-contributor-policy.md`, "Which document settles what", and
  `docs/tickets/README.md`.
- [ ] AC7: every substantive new rule has a `Retired when:` line; the fifth
  review found three mutations leave other supporting wording intact. The
  blocker above records the required repair and next review.

### Falsification

The reproducible PowerShell command in "How to verify" checks each claim in
the table independently, then replaces that claim's required text in memory.
Run after `12796ab`, it passed 17 baseline checks and rejected 17 mutations;
that commit is the baseline for every count in this section.

| Claim | Mutant | Red |
|---|---|---|
| Template requires `why:` | replace with `reason:` | 1 of 1 |
| Template requires the causal section | rename its heading | 1 of 1 |
| Causal section requires evidence | replace its evidence instruction | 1 of 1 |
| Lifecycle includes `system-unavailable` | replace the value | 1 of 1 |
| Lifecycle includes `multi-feature-blocking` | replace the value | 1 of 1 |
| Lifecycle includes `feature-blocking` | replace the value | 1 of 1 |
| Lifecycle includes `degraded` | replace the value | 1 of 1 |
| Lifecycle includes `enhancement` | replace the value | 1 of 1 |
| Template defines a vertical slice | replace its definition | 1 of 1 |
| Template defines enabling work | replace its definition | 1 of 1 |
| Scheduling policy requires an action boundary | rename its heading | 1 of 1 |
| Action boundary preserves human authority | replace its prohibition | 1 of 1 |
| Scheduling template cannot replace canonical order | replace its statement | 1 of 1 |
| Lifecycle chooses greatest allowed impact first | replace its statement | 1 of 1 |
| Tier model prohibits impact-driven tier changes | replace its prohibition | 1 of 1 |
| Contributor policy prohibits impact inference | replace its prohibition | 1 of 1 |
| Governed-document map includes selection | remove `select` | 1 of 1 |

### Out of scope (per ticket)

- No scheduler, parser, dispatch mechanism or merge authority was implemented.
- No project received unattended authority.
- Existing real tickets were not reclassified; EM-022-001 records the example
  update separately.

### How to verify

1. Run `git diff --check main...HEAD`.
2. Run this non-mutating PowerShell command from the repository root. It reads
   the current files, asserts seventeen independent baseline claims, then asserts that seventeen
   in-memory counterfactuals are rejected:

```powershell
function Require([bool]$condition, [string]$name) {
    if (-not $condition) { throw "baseline failed: $name" }
}

$sources = @{
    template = Get-Content -Raw templates/TICKET.md
    lifecycle = Get-Content -Raw docs/ticket-lifecycle.md
    tier = Get-Content -Raw docs/tier-review-model.md
    schedule = Get-Content -Raw templates/SCHEDULING-POLICY.md
    policy = Get-Content -Raw docs/ai-contributor-policy.md
}
$claims = @(
    @{ name = 'why field'; source = 'template'; required = 'why:'; replacement = 'reason:' },
    @{ name = 'causal section'; source = 'template'; required = '## Why this ticket should be worked'; replacement = '## Ticket rationale' },
    @{ name = 'evidence instruction'; source = 'template'; required = 'evidence for that claim'; replacement = 'opinion about that claim' },
    @{ name = 'system unavailable'; source = 'lifecycle'; required = 'system-unavailable'; replacement = 'system-paused' },
    @{ name = 'multi-feature blocking'; source = 'lifecycle'; required = 'multi-feature-blocking'; replacement = 'multi-feature-paused' },
    @{ name = 'feature blocking'; source = 'lifecycle'; required = 'feature-blocking'; replacement = 'feature-paused' },
    @{ name = 'degraded'; source = 'lifecycle'; required = 'degraded'; replacement = 'impaired' },
    @{ name = 'enhancement'; source = 'lifecycle'; required = 'enhancement'; replacement = 'improvement' },
    @{ name = 'slice definition'; source = 'template'; required = 'thinnest independently demonstrable end-to-end'; replacement = 'separate component' },
    @{ name = 'enabling definition'; source = 'template'; required = 'without itself being end-to-end'; replacement = 'as a separate component' },
    @{ name = 'action-boundary heading'; source = 'schedule'; required = '## Authorised action boundary'; replacement = '## Action boundary' },
    @{ name = 'human-authority limit'; source = 'schedule'; required = 'cannot grant a human authorisation'; replacement = 'may grant a human authorisation' },
    @{ name = 'template order limit'; source = 'schedule'; required = 'This policy chooses eligibility, not a replacement order.'; replacement = 'This policy may replace the impact order.' },
    @{ name = 'lifecycle impact order'; source = 'lifecycle'; required = 'greatest allowed impact first'; replacement = 'lowest allowed impact first' },
    @{ name = 'tier independence'; source = 'tier'; required = 'cannot raise or lower the tier'; replacement = 'can lower the tier' },
    @{ name = 'no impact inference'; source = 'policy'; required = 'Do not infer, upgrade or downgrade a ticket'; replacement = 'Infer, upgrade or downgrade a ticket' },
    @{ name = 'document map'; source = 'policy'; required = 'How do I claim, select, block, batch and close work'; replacement = 'How do I claim, block, batch and close work' }
)

foreach ($claim in $claims) {
    $source = $sources[$claim.source]
    Require ($source.Contains($claim.required)) $claim.name
    $mutant = $source.Replace($claim.required, $claim.replacement)
    if ($mutant.Contains($claim.required)) { throw "mutant accepted: $($claim.name)" }
    Write-Output "red: $($claim.name)"
}
```

### Risks / follow-ups

- EM-022-001 is blocked until this rule reaches the default branch; it will
  align published ticket examples with the new template.
- OMNISSIAH suggestion SUG-002 records implementation of the deterministic
  scheduler as separate, unauthorised future work.

### Review

| Round | Must-fix | Where (rules / lists / documents / tests) | Inside previous round's fix | Repaired by |
|---|---:|---|---|---|
| 1 | 5 | board index; child-ticket lifecycle; template classification; impact ordering; rule falsifiers | — | `91c2bd7` |
| 2 | 1 | contributor-policy document map | no | `093e430` |
| 3 | 1 | reproducible per-claim falsification evidence | no | `5fe7998` |
| 4 | 1 | falsification mutations cover claim fragments, not whole compound claims | no | `12796ab` |
| 5 | 1 | three claim mutations leave alternate supporting wording intact | no | — |
