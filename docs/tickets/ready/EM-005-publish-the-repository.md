---
id: EM-005
title: Publish the repository to a public host
status: ready
tier: critical
complexity: S
dependencies: [EM-003]
claimed_by: maintainer
claimed_at: 2026-08-31
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

1. **Repository name.** ~~Undecided.~~ **Resolved 2026-08-31: `countersign`**,
   chosen by the maintainer. Named for the separation-of-duties rule — a
   second, independent signature required before work takes effect. The local
   directory is renamed to match. AC2 is met.
2. **Hosting account.** ~~Undecided.~~ **Resolved 2026-08-31: `callum-johnson`**,
   an account created for the purpose. This satisfies the audit prerequisite by
   construction rather than by work — a new account carries no other
   repositories, so publishing here exposes nothing that has not been assessed.

   The 2024 project described in `case-studies/00-growth-2024-2026.md` — the
   one with a committed development TLS key and five host-disclosing crash
   dumps — remains private under a separate account and is unaffected by this
   decision. It is named in the case study but not linked, and nothing in this
   repository points a reader to it.

**Unblocked 2026-08-31.** Both maintainer decisions are recorded above. The
remaining work is the push itself, which is the maintainer's to perform: it is
irreversible in the way that matters, and the executor does not publish on the
maintainer's behalf.
