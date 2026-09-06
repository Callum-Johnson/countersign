---
id: EM-005-001
title: Link commit authorship to the publishing account
status: ready
tier: trivial
complexity: S
dependencies: [EM-005]
---

# EM-005-001 — Link commit authorship to the publishing account

## Context

Raised while working EM-005. Commits are authored `Callum Johnson
<meuwhowhatwherey@googlemail.com>`, which is correct. That address is not
verified under the publishing account, so the host renders every commit as an
unattributed name with no avatar and no profile link.

On a repository published as evidence of how its author works, commits that do
not visibly belong to that author undercut the point.

## Specification

Add and verify the authoring address under the account's email settings. No
repository change is required — attribution is retroactive once the address is
verified.

## Acceptance criteria

1. AC1: The authoring address is listed and verified under the account.
2. AC2: All existing commits render as the linked account, with avatar.
3. AC3: `git log -1 --format=%ae` still returns the same address, confirming
   no rewrite was needed.

## Out of scope

- Rewriting existing commits or their authorship. The fix is account-side.
- Changing the repository's local `user.email`.

## References

- EM-005

## Notes

Maintainer action; not executable from the working environment.

**Measured 2026-09-06 at 0947dda, via the host's public commit API.** The
authoring address now resolves to a linked account — but not to the
publishing account. The address is verified under a different, older account
of the maintainer's, so every commit here renders with that account's avatar
and profile link rather than `callum-johnson`'s. AC1 is therefore not met as
written, and the state is arguably worse than unattributed: EM-005 chose a
new account so that publishing here would expose nothing unassessed, and the
commit attribution now points a reader at an account that decision did not
audit. The remedy is still account-side — move the verified address to the
publishing account, or record here that the attribution is accepted and why.
The other account is deliberately not named in this file.
