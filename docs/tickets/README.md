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
| EM-004 | active | standard | Add per-project case studies |
| EM-005 | done | critical | Publish the repository |
| EM-005-001 | ready | trivial | Link commit authorship to the publishing account |
| EM-006 | ready | critical | Falsification gate; correct three published patterns that do not compose |
| EM-007 | ready | critical | State when an independent review ends |
| EM-008 | ready | critical | A decision reserved to another party is handled as ambiguity |
| EM-009 | ready | critical | A review finding is repaired at its class, falsified per sibling |
| EM-010 | ready | critical | A review answers two questions; over-tightening is a finding |
| EM-011 | ready | critical | Review runs in its own worktree; the tree is checked afterwards |
| EM-012 | ready | critical | Trivial changes are batched into one ticket |
| EM-013 | ready | standard | Assess the methodology against ISO/IEC 42001 |
| EM-014 | ready | critical | A rule states its own falsifier; a control can be retired |
| EM-014-001 | ready | critical | Both columns on one rule in consecutive rounds is a class signal |
| EM-015 | ready | trivial | The README states two commit counts for one project |

EM-001 and EM-002 are retrospective and say so in their bodies. They are not
backdated; ADR-0001 explains why backdating was rejected.
