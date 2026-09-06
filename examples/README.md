# Real artifacts

Ten artifacts from a private project, published because they concern software
architecture and workflow only. See [DISCLOSURE.md](../DISCLOSURE.md) for how
they were selected and what was excluded.

Project names and ticket identifiers are normalised. Nothing else was changed
at publication, and nothing within a published file is redacted. One dated
annotation was added later, under its own heading, to `adr-0038`; see
[DISCLOSURE.md](../DISCLOSURE.md) for why.

## Decision records

| File | Why it is here |
|---|---|
| [`adr-0038`](adr/adr-0038-tickets-carry-the-lineage-of-the-ticket-that-raised-them.md) | The ticket lineage scheme, decided and recorded as an ADR. The clearest example of the process governing itself. Carries a dated annotation at the end, added under EM-006, correcting its lookup instructions; the original text is unchanged. |
| [`adr-0019`](adr/adr-0019-a-non-committing-validate-endpoint.md) | Adding an endpoint that answers "would this be legal?" without mutating state — a contract decision, reasoned through alternatives. |
| [`adr-0018`](adr/adr-0018-the-adapter-states-a-cors-policy.md) | A CORS decision that starts by questioning whether the concern belongs to this component at all, and records the negative consequences of the answer honestly. |

## Tickets

| File | Why it is here |
|---|---|
| [`PRJ-001`](tickets/PRJ-001-repo-skeleton.md) | The first ticket on the project. Shows the template in use from commit one, not retrofitted. |
| [`PRJ-011`](tickets/PRJ-011-pr-md-workflow-fix.md) | A fix to the pull-request workflow itself, raised and tracked as ordinary work. |
| [`PRJ-012`](tickets/PRJ-012-frontmatter-status-on-close.md) | Enforcing the directory/status invariant — the process catching its own drift. |
| [`PRJ-034`](tickets/PRJ-034-ci-gate-ai-package.md) | Extending the CI gates to a new package. |
| [`PRJ-035`](tickets/PRJ-035-action-protocol-variance.md) | A typing-variance problem, specified precisely enough for an agent to implement without interpretation. |
| [`PRJ-161`](tickets/PRJ-161-package-runtime-ai.md) | Packaging work with an explicit out-of-scope list. |
| [`PRJ-175`](tickets/PRJ-175-cors-middleware.md) | The implementation ticket paired with `adr-0018` — read them together to see the decision-to-work path. |

## What to look at

If you only read two, read **`adr-0038`** and **`PRJ-012`**. Between them they
show the thing this repository is actually about: a process that generates
tickets and decision records *about itself*, and treats its own integrity
failures as tracked work rather than as tidying.
