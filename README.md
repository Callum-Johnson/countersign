# Countersign

How I run software projects where most of the code is written by AI agents:
the ticket that binds them, the policy that constrains them, and the second
signature that lets their work merge.

The name is the rule the repository is built around: work that alters an
existing contract does not merge on the say-so of the agent that produced it.
It requires a countersignature — a reviewer that is not the executor, and that
has not seen the executor's reasoning.

This repository documents **process, not product**. The projects it draws on
are private. What is published here is the operating system around them — the
templates, policies and workflow rules — plus a small set of genuine artifacts
that contain no third-party material. See [DISCLOSURE.md](DISCLOSURE.md) for
what is withheld and why.

---

## Why this exists

Most "I use AI to code" claims are unfalsifiable. This is the opposite: a
written policy, a ticket lifecycle with an enforced state machine, a tiered
review model, and CI gates — applied continuously to a codebase that reached
1,879 commits in two months.

The interesting problem is not getting an agent to write code. It is stopping
a fleet of them from quietly destroying a codebase while doing so.

---

## Start here

| Document | What it covers |
|---|---|
| [AI contributor policy](docs/ai-contributor-policy.md) | The rules AI agents work under: scope limits, forbidden actions, the escalation protocol, the pre-flight checklist |
| [Ticket lifecycle](docs/ticket-lifecycle.md) | How work is defined, claimed, blocked, and closed — and the directory/status invariant that keeps it honest |
| [Tier review model](docs/tier-review-model.md) | Three risk tiers, the operative test that assigns them, and what each demands |
| [Quality gates](docs/quality-gates.md) | What must pass before merge, and why each gate is there |
| [ADR process](docs/adr-process.md) | When a decision is architectural, and how it gets recorded |
| [Disclosure policy](DISCLOSURE.md) | What is withheld from this repository, and the reasoning |

Templates are in [`templates/`](templates/). Real artifacts that were safe to
publish are in [`examples/`](examples/).

## This repository runs on its own process

Work here is tracked as tickets and decisions, in the system this repository
documents — see [the board](docs/tickets/README.md) and
[the decision records](docs/adr/).

It did not start that way. The initial commit landed 2,540 lines with no ticket
and no decision record, which is visible in the git history and is the first
thing worth checking about a repository like this.
[ADR-0001](docs/adr/0001-this-repository-is-governed-by-the-process-it-documents.md)
records adopting the process and rejects backdating tickets to cover the gap.
[ADR-0002](docs/adr/0002-critical-tier-review-in-a-single-maintainer-repository.md)
deals with the awkward consequence: a single maintainer cannot satisfy the
model's own two-reviewer rule.

---

## The core ideas

**1. No shared memory.** Every agent is assumed to have zero context from any
previous session. Anything the next contributor needs lives in the repository —
a ticket, an ADR, or a comment about a non-obvious invariant. Never in a chat
log. This one rule generates most of the others.

**2. The ticket is the contract.** An agent may implement what the ticket
specifies and nothing else. Discovered work becomes a new ticket with recorded
lineage; it does not get silently fixed. Ambiguity is escalated, never resolved
by invention.

**3. State is stored twice and must agree.** A ticket's `status:` field and the
directory it sits in are the same fact. Every move pairs the two in a single
commit, so the workflow cannot drift out of sync without leaving evidence.

**4. Risk tier is decided by a test, not a feeling.** *Could an existing caller
or a seeded roll notice this change without opting in?* Yes means critical and
a second reviewer. No means standard. Touching an important file is a prompt to
run the test, not an automatic escalation.

**5. Gates are machine-checked.** Lint, format, strict type-checking and tests
run identically on a contributor's machine and in CI. An agent cannot talk its
way past a failing gate, and skipping hooks is a forbidden action.

---

## Where this came from

The practice developed across three projects over two years. The change is
visible in the artifacts:

| | Prose generation tool | AI CV product | Rules engine + client |
|---|---|---|---|
| **Period** | Jun – Nov 2024 | Feb – Jun 2026 | Jun – Aug 2026 |
| **Commits** | 11 | 183 | 2,294 |
| **Tests** | 3 files | 27 files + CI | 276 files |
| **Decision records** | none | none | 39 ADRs |
| **Tracked tickets** | none | 32 (as branches) | 292 closed (as files) |
| **Agent policy** | none | contributing guide | enforced, with checklist |
| **Secrets hygiene** | a TLS key and host crash dumps committed | clean | clean, and policy-enforced |

The 2024 project had a stock framework README and commit messages reading
"no idea, getting better though". It also committed a development TLS key and
five JVM crash dumps that disclosed the host's full `PATH`, username and
installed software versions.

I found that by auditing my own repositories. It is included here deliberately:
the interesting part of a methodology is not the polished end state, it is
knowing what it corrects.

See [the growth case study](case-studies/00-growth-2024-2026.md) for detail.

---

## Licence

Documentation and templates: [CC BY 4.0](LICENSE). Use them, adapt them,
credit is appreciated but the templates are meant to be stolen.
