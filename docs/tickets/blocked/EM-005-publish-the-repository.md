---
id: EM-005
title: Publish the repository to a public host
status: blocked
tier: critical
complexity: S
dependencies: [EM-003]
claimed_by: maintainer
claimed_at: 2026-08-31
blocked_at: 2026-08-31
---

# EM-005 — Publish the repository to a public host

## Context

The repository is complete enough to publish: policy documents, templates, ten
cleared artifacts, a disclosure policy and a licence. It has no remote, so no
accidental push is possible.

Publication is irreversible in the way that matters — a public commit is
mirrored, cached and indexed within minutes, and deleting the repository
afterwards does not retract it.

## Specification

Create the public repository, push, and confirm the rendered result.

## Acceptance criteria

1. AC1: A final proprietary-term scan runs against the exact tree being
   pushed, and returns zero matches.
2. AC2: The repository name is decided and recorded here.
3. AC3: The remote is added and the initial history pushed.
4. AC4: The rendered README and every internal link are checked in the
   browser, not only locally.

## Out of scope

- Publishing any source repository. This repository only.

## References

- `DISCLOSURE.md`
- ADR-0001

## Notes

BLOCKER: two decisions are the maintainer's and cannot be made by an executor.

1. **Repository name.** `engineering-methods` is the working name. It is
   accurate and forgettable, and the name is the first thing a reader
   evaluates.
2. **Hosting account.** Publishing under an account that also carries older
   repositories exposes those to the same reader. The 2024 project described
   in `case-studies/00-growth-2024-2026.md` has a committed development TLS
   key and five host-disclosing crash dumps, and is currently not public. If
   it were to become public, or if other repositories on the account have not
   been audited, that audit is a prerequisite and not part of this ticket.

Blocked pending both. Per `docs/ai-contributor-policy.md` §3, the executor
does not choose on the maintainer's behalf.
