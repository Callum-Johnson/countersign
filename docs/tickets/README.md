# Tickets

Work on this repository is tracked here, per ADR-0001.

| Directory | Meaning |
|---|---|
| `ready/` | Specified, dependencies met, available to claim |
| `active/` | Claimed and in progress |
| `blocked/` | Cannot proceed; carries a `BLOCKER:` note |
| `done/` | Merged, with the pull-request description appended |

Each ticket's `status:` frontmatter and its directory are the same fact stored
twice and must always agree. See [ticket lifecycle](../ticket-lifecycle.md).

The template is [`templates/TICKET.md`](../../templates/TICKET.md).

## Current board

| Ticket | State | Tier | Summary |
|---|---|---|---|
| EM-001 | done | critical | Triage source artifacts for third-party IP (retrospective) |
| EM-002 | done | standard | Publish policy documents, templates and cleared examples (retrospective) |
| EM-003 | done | critical | Adopt the documented process in this repository |
| EM-001-001 | done | standard | Harden the IP classifier and make the triage reproducible (closed 2026-09-15 without the work; the maintainer declined a script in this repository) |
| EM-001-001-001 | ready | standard | The lifecycle has no close for a ticket that will not be worked |
| EM-004 | blocked | standard | Add per-project case studies |
| EM-005 | done | critical | Publish the repository |
| EM-005-001 | ready | trivial | Link commit authorship to the publishing account |
| EM-006 | done | critical | Falsification gate; correct three published patterns that do not compose |
| EM-006-001 | done | critical | The README and the tier model say every gate is machine-checked; one now is not |
| EM-007 | done | critical | State when an independent review ends |
| EM-007-001 | done | trivial | The lifecycle's list of pull-request description sections is behind the template |
| EM-008 | done | critical | A decision reserved to another party is handled as ambiguity |
| EM-009 | done | critical | A review finding is repaired at its class, falsified per sibling |
| EM-010 | done | critical | A review answers two questions; over-tightening is a finding |
| EM-010-002 | done | trivial | ADR-0002 lags the model on what the reviewer receives |
| EM-011 | done | critical | Review runs in its own worktree; the tree is checked afterwards |
| EM-012 | done | critical | Trivial changes are batched into one ticket |
| EM-012-001 | done | critical | The tier model does not say how trivial is distinguished from standard |
| EM-012-001-001 | done | trivial | The batch entry's supporting answer is still the standard-tier answer |
| EM-013 | blocked | standard | Assess the methodology against ISO/IEC 42001 |
| EM-014 | done | critical | A rule states its own falsifier; a control can be retired |
| EM-014-001 | done | critical | Both columns on one rule in consecutive rounds is a class signal |
| EM-015 | ready | trivial | The README states two commit counts for one project |
| EM-016 | done | critical | Bound the brief a contributor must read |
| EM-016-001 | done | trivial | The README's document table is a third description the rule does not bind |
| EM-016-001-001 | done | trivial | The README's fourth core idea names two tiers of three |
| EM-017 | done | trivial | Batch — trivial changes, 2026-09-06 |
| EM-018 | done | standard | The templates cite files this repository does not publish |
| EM-019 | done | trivial | Three figures in EM-016's closed description were predicted, not measured |
| EM-019-001 | done | critical | A reported figure is read from a command, not written by its author |
| EM-019-001-001 | done | critical | Rule-adding tickets produce no decision record, against the trigger list |
| EM-019-001-001-001 | done | critical | The decision-record test reads wider than the line drawn beneath it |
| EM-018-002 | done | standard | The ADR template restates the decision-record test in its superseded form |
| EM-018-003 | ready | standard | The ADR template's trigger lists disagree with the document in both directions |
| EM-020 | done | critical | Read the whole thing before acting on part of it |
| EM-021 | done | critical | A rule needs a second instance before it is written |
| EM-022 | done | critical | Define ticket rationale, impact and unattended selection |
| EM-022-001 | blocked | trivial | Update ticket examples for rationale and impact metadata |
| EM-020-001 | blocked | critical | A review must-fix on a sentence the ticket's Behaviour dictates is taken in the round and recorded (answered (a) on 2026-09-15; assigned to the maintainer, not claimable by an agent executor) |
| EM-007-002 | done | standard | A process-document change is trivial by the test and critical by ADR-0002 |
| EM-007-002-001 | done | standard | The operative test's one-line summary omits the process-surface clause |
| EM-007-002-002 | done | standard | The ADR process states the wider reading the model no longer holds |
| EM-007-002-003 | done | standard | Clause 5 of the operative test still names a change to the review model as critical |
| EM-007-002-003-001 | done | standard | ADR-0004 reads proposed while its decision is in force |
| EM-007-002-003-002 | ready | standard | ADR-0004's annotation says the status is unchanged and the status has changed |
| EM-009-001 | done | critical | The class obligation binds every repaired finding |
| EM-018-001 | done | standard | The ticket template's how-to-use steps disagree with the lifecycle on three points |
| EM-023 | done | standard | The next-id command misses an id created by renaming a ticket file |
| EM-023-001 | done | trivial | The ADR-0038 correction rewrote a dated annotation instead of adding one |
| EM-023-002 | done | trivial | The disclosure counts one post-publication annotation and there are now two |
| EM-024 | in-progress | critical | A count written into prose has no falsifier and drifts silently |
| EM-024-001 | active | standard | The tier model restates a count beside its own list |
| EM-024-002 | done | standard | The gate count is restated away from its site, and it is not alone |
| EM-025 | done | standard | The per-round table has one copy, and the blocker names the row |
| EM-026 | active | standard | An exhaustive claim is derived, not listed |

EM-001 and EM-002 are retrospective and say so in their bodies. They are not
backdated; ADR-0001 explains why backdating was rejected.
