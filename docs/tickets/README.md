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
| EM-001-001 | blocked | standard | Harden the IP classifier and make the triage reproducible |
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
| EM-016 | ready | critical | Bound the brief a contributor must read |
| EM-017 | active | trivial | Batch — trivial changes, 2026-09-06 |
| EM-018 | ready | standard | The templates cite files this repository does not publish |
| EM-007-002 | blocked | critical | A process-document change is trivial by the test and critical by ADR-0002 |
| EM-009-001 | blocked | critical | The class obligation binds every repaired finding |

EM-001 and EM-002 are retrospective and say so in their bodies. They are not
backdated; ADR-0001 explains why backdating was rejected.
