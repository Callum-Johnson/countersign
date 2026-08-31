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
| EM-001-001 | ready | standard | Harden the IP classifier and make the triage reproducible |
| EM-004 | ready | standard | Add per-project case studies |
| EM-005 | done | critical | Publish the repository |
| EM-005-001 | ready | trivial | Link commit authorship to the publishing account |

EM-001 and EM-002 are retrospective and say so in their bodies. They are not
backdated; ADR-0001 explains why backdating was rejected.
