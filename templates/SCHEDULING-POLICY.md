# Project scheduling policy

Copy this template into the adopting project's durable policy record before
automatic ticket selection is enabled. Fill every section; write `N/A` only
where the section does not apply.

This policy authorises selection only. It does not alter the ticket lifecycle,
risk tier, gates, review requirements, human-authorisation requirements or
merge authority.

## Eligible impact

List the `impact` values an unattended selector may choose, in the order this
project permits. A selector may consider no other value.

- `system-unavailable`
- <other permitted values, or `N/A`>

## Concurrency limit

State the maximum number of unattended tickets that may run at once and why
the project can safely support it.

<positive integer and rationale>

## Deterministic tie-breaker

State the stable fact used when eligible tickets have the same impact. It must
be computable from the repository or the policy, not from an agent's judgement.

<for example: lexicographic ticket identifier>

## Stop and notify conditions

State which outcomes stop selection entirely, pause only the affected ticket,
and notify the maintainer. At minimum address a blocker, policy refusal, gate
failure, missing approval and exhausted concurrency.

<conditions and action>

## Authorised action boundary

State exactly what automatic selection may cause: for example, "dispatch to a
ticket branch only". State separately any later action that remains manual.
A policy cannot grant a human authorisation that Countersign or the adopting
project reserves to a person.

<authorised and excluded actions>

## Review and review date

Name who approved this policy, when it is next reviewed, and the evidence that
would cause its eligible impacts, concurrency or tie-breaker to change.

<approval and review trigger>

**Retired when:** the adopting project stops using automatic ticket selection,
or the ticket lifecycle defines a repository-native scheduling policy with the
same authority boundary; this template then adds a second policy record.
