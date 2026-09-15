---
id: EM-026
title: An exhaustive claim is derived, not listed
status: done
tier: standard
complexity: S
dependencies: []
claimed_by: claude-opus-5
claimed_at: 2026-09-15
closed_at: 2026-09-15
claimed_by:
claimed_at:
closed_at:
---

# EM-026 — An exhaustive claim is derived, not listed

## Context

The falsification gate asks for a red count per claim and says a zero means
the test is decorative. It does not cover the case where the count is
**non-zero and the claim is still unpinned**, because the check and the
property are joined by a list the author wrote.

Four instances on OMNISSIAH, in four tickets, each found by a different
reviewer, between 2026-09-08 and 2026-09-15. In every one the suite was green,
the falsification count was recorded, and the property the test named was
absent.

| Ticket | The check | What the list missed |
|---|---|---|
| OMN-024, round 4 | `test_nothing_in_src_constructs_a_gate_runner` | population taken from calls whose `func` is a bare `ast.Name`; an **attributed** call escapes |
| OMN-034, AC5 | one helper guard plus two AST sweeps, certifying that no test starts a real agent | the reviewer used `subprocess.run` with a program name built as `"cla" + "ude"`, reached the host's real `claude.EXE` **while the certifying test stayed green** |
| OMN-020-002 | `test_every_spawn_site_that_runs_chosen_code_builds_its_environment` | iterates a hardcoded two-module tuple and matches only `subprocess.Popen`; missed a third site using `subprocess.run`, which handed a child 92 environment variables including a secret |
| OMN-038, AC4 | `test_a_reviewer_named_as_its_own_subject_is_refused` | the rival reddens it, so the count is 1 — but the test calls the function directly with an id no caller can supply, so **the path it pins is unreachable** |

The third is the sharpest on authorship: the executor wrote the limitation
into the test's own docstring — *"The enumeration pins the declared set; it
cannot see a third spawn site written without consulting it"* — and asserted
the completeness claim in module text anyway, on a governance surface, inside
a signed diff.

The fourth is the sharpest on the gate: every signal was green. The test
passed, the rival reddened it, the count was recorded and non-zero, and the
property — that a reviewer cannot name itself as its own subject — did not
hold for any caller that exists.

**The remedy is already known**, because OMN-034's repair found it. The guard
moved from three source-shaped checks to `subprocess.Popen.__init__`, the one
place every subprocess in the process converges, with the allowlist
**measured from an instrumented run** rather than guessed — 12,813 `git`
spawns, 179 `python.exe`, 18 `taskkill`. What made it work was not more care
about the list. It was not having a list.

## Specification

One rule in `docs/quality-gates.md`, beside the falsification gate, since it
is that gate's uncovered case rather than a new obligation.

### Files

- `docs/quality-gates.md` — the rule, after "The falsification gate"

No other document is edited. If the rule cannot be stated without amending
`docs/tier-review-model.md` or `docs/ai-contributor-policy.md`, that is a
finding and it stops and asks.

### The rule to land

Its content, not its wording. Whoever claims this writes it.

**A test that asserts something of *every* member of a population must derive
that population from the thing it describes, not restate it.** Three tiers,
in order of preference, because the first is not always available:

1. **Assert at the convergence point.** Where every member must pass through
   one place, check there. A population that cannot be enumerated wrongly
   beats one enumerated carefully.
2. **Derive the population.** Walk the tree, read the registry, ask the
   module — do not list the files, the call shapes, or the spellings.
3. **Where neither is possible, the docstring says what the check cannot
   see**, and *that* statement is itself pinned — the shape the falsification
   gate already uses for a non-discriminating test.

And the clause the fourth instance adds: **a rival must redden a path a
caller can take.** A count earned only through an entry point no caller
reaches is a zero wearing a number, and the gate's existing sentence — "a zero
written down is a fact a reviewer can act on" — does not reach it, because
nothing was written down as zero.

### What this rule is not

- **Not a ban on structural tests.** All four instances are worth keeping.
  The rule is about what makes their claim true, not about deleting them.
- **Not a demand for exhaustive proof.** Tier 3 is a real answer, and stating
  a gap honestly is what OMN-020-002 did right about network enforcement
  while doing it wrong about spawn sites — in the same file, on the same day.
- **Not retrospective.** It binds checks written after it lands. Nothing
  sweeps the existing corpus for lists.

### Falsification

The gate's own obligation applies to this ticket, and the honest difficulty
is stated rather than discovered: **this is a prose rule in a documentation
repository, and there is no suite for a sentence to redden.** What can be
done and should be:

- The rule is applied to the four instances above and asked whether it would
  have caught each. **If it would not have caught one, that is recorded, not
  smoothed** — a rule that catches three of four is still worth landing and
  the fourth is what retires it.
- The wording is checked against the falsification gate for contradiction. If
  the two disagree about what a zero means, one of them is wrong and this
  ticket says which.

**Retired when:** over a stated population of reviews, a check written after
this rule is found to have derived its population and still missed a member —
the rule would then be asking for the wrong thing rather than for more care.
Or: no reviewer finds a written-down population over a stated population of
changes, at which point the rule is a restatement of practice and leaves.

## Acceptance criteria

1. AC1: the rule is in `docs/quality-gates.md`, stating the three tiers and
   the reachable-path clause.
2. AC2: it is applied to all four instances in Context, and the answer for
   each — would this rule have caught it — is recorded, including any "no".
3. AC3: `git diff main...<branch> --name-only` names `docs/quality-gates.md`
   and the ticket file and nothing else, with the command and the head.
4. AC4: the rule does not contradict "The falsification gate"; the check is
   named in the description rather than asserted.
5. AC5: `standard` per EM-007-002 — one independent pass, closes on it, and
   the executor may not raise the tier.

## Out of scope

- Any change to the falsification gate's own text. This sits beside it.
- Sweeping OMNISSIAH's existing tests. The four instances are evidence, not
  a work list; three already have their own repairs.
- The review-debt observation from 2026-09-14 — that a review which happened
  but cannot be recorded should be recorded as a debt. **One day, four
  instances, all in one project and all caused by one absent capability**
  (nothing could create a reviewer run). It does not meet the second-instance
  bar as a *methodology* finding and is deliberately left out; it is named
  here so a later reader knows it was considered and why it was not taken.

## References

- `docs/quality-gates.md`, "The falsification gate" — the rule this extends,
  and its existing treatment of a zero and of a non-discriminating test
- OMNISSIAH OMN-024, OMN-034, OMN-020-002, OMN-038 — the four instances
- OMNISSIAH `tests/conftest.py`, `SPAWNABLE` and the `subprocess.Popen.__init__`
  guard — the remedy that worked, and the measurement behind its allowlist
- EM-007-002 — process-document changes are `standard`, one pass

## Notes

Raised on 2026-09-15 at the maintainer's request, after a day on OMNISSIAH in
which the same shape was found three times. The fourth instance arrived while
this ticket was being drafted.

**Tier: `standard`**, per EM-007-002: a process-document change takes one
independent pass and closes on it, and the executor may not raise it.

**The 2026-09-10 moratorium is discharged.** The maintainer's direction then
was that EM-025 would be the last rule-about-records ticket **until the
product had run once**. OMNISSIAH dispatched a real agent against a throwaway
repository on 2026-09-14 and it completed; the mediated chain — dispatch,
refuse, review, close, merge — ran end to end the same day. This rule is also
about tests rather than about records, which is the kind the 2026-09-10
review found was earning its keep.

## PR Description

### Ticket
EM-026 — An exhaustive claim is derived, not listed.

### Tier
`standard`, on one independent review pass, per EM-007-002 and ADR-0004. A
change to `docs/quality-gates.md` is a change to a process document; the tier
is fixed there and is not the executor's to raise. The pass ran against
3bf3f62 and is row 1 of the Review table.

### Summary
The falsification gate asks what a wrong implementation would redden. It does
not reach the case where the count is non-zero and the claim is still unpinned,
because the check and the property it names are joined by a list the author
wrote: the rival reddens the members the list happens to hold, and a member
outside it escapes with the suite green. The rule lands beside the gate, with
a reach test, three tiers, the reachable-path clause and a falsifier per
obligation.

### Acceptance criteria
- [x] AC1: the rule is in `docs/quality-gates.md`, stating the three tiers and
  the reachable-path clause. Tiers 1 to 3 are numbered and ordered, with the
  reason for the ordering; the reachable-path clause is its own bolded
  sentence. Both sit inside "The falsification gate" — see the placement note
  under AC3.
- [x] AC2: applied to all four instances in Context, with the answer for each
  recorded, including the "no". **The rule was written from these four, so the
  question was asked adversarially — does the rule's own wording reach each
  instance, not does the instance sound like the rule.**

  | Instance | Caught? | By which part |
  |---|---|---|
  | OMN-024 round 4 — population taken from calls whose `func` is a bare `ast.Name`; an attributed call escapes | Yes | **Tier 2, not cleanly the headline.** The check did walk the tree, so "derives that population" is arguably satisfied on a literal reading — what was restated was the match predicate, not the file set. Tier 2's "do not list the call shapes" is what lands it; tier 1 is what would have fixed it. |
  | OMN-034 AC5 — one helper guard and two AST sweeps certifying no test starts a real agent; a reviewer reached the real binary with a name built as `"cla" + "ude"` while the certifying test stayed green | Yes | Headline reaches it — the population is every test that starts a real agent, and the sweeps restated it as source shapes. Tier 2's "spellings" names the exact escape. Tier 1 is the repair that actually worked: the guard moved to `subprocess.Popen.__init__`, the point every subprocess converges. |
  | OMN-020-002 — a hardcoded two-module tuple matching only `Popen`, missing a third site using `subprocess.run` that handed a child 92 environment variables including a secret | Yes | Headline reaches it directly; this is the paradigm case. The round-1 reviewer found that tier 3 as first written let this author take the same escape they had already taken — a docstring beside a written list, with tier 1 available all along. Tier 3 now requires the author to say why tiers 1 and 2 were unavailable, which is what makes the letter and the practice agree here. |
  | OMN-038 AC4 — the rival reddens, so the count is 1, but the test calls the function directly with an id no caller can supply | **No, by the headline.** Caught only by the reachable-path clause. | **This is the "no" the ticket asks be recorded rather than smoothed.** There is no exhaustive claim and no population in this instance: run the headline sentence over that test and it returns nothing. The fourth instance is carried entirely by a clause bolted beside the rule rather than by the rule the ticket is named for. That is also why the round-1 reviewer's R1.4 mattered — the bolted-on clause was the one shipping without a falsifier of its own, and it now has one. |

  Four of four are caught by the rule as a whole; three of four by its headline;
  one of those three (OMN-024) only once tier 2 is read.
- [x] AC3: the branch diff names the document, the ticket file and the board
  row. `git diff main...HEAD --name-only`, run after de01d1a, returns
  `docs/quality-gates.md`, `docs/tickets/README.md` and
  `docs/tickets/active/EM-026-an-exhaustive-claim-is-derived-not-listed.md`.

  AC3's literal words name two paths. The third is `docs/tickets/README.md`,
  which the lifecycle's claim step requires in the same commit as the move to
  `active/` and which the close step requires again; it is a board row, not a
  document that states rules, and the ticket's own Files line — "No other
  document is edited" — is the criterion's intent and is met. No document
  under `docs/` or `templates/` other than `docs/quality-gates.md` is touched.

  **Placement, and why no map or index edit was owed.** The rule is a bolded
  paragraph inside "The falsification gate", not a new `##` section. That is
  what the Specification asks for — "beside the falsification gate, since it is
  that gate's uncovered case rather than a new obligation" — and it copies the
  form the gate already uses for its companion rule, "A test pins a claim, not
  a mechanism". "Keeping the map true" fires on "a section added to, removed
  from or renamed in a governed document that carries an index": no section was
  added — `grep -c '^## ' docs/quality-gates.md` returns 9 before and after —
  and that document carries no index, so the trigger cannot fire on either
  ground. The map row for `docs/quality-gates.md` asks "what does the
  falsification gate ask of me", and this is one more thing the gate asks,
  still settled in the same document, so the question the row settles is
  unchanged. The Specification's stop-and-ask condition — if the rule cannot be
  stated without amending the tier model or the contributor policy — was not
  reached.
- [x] AC4: the rule does not contradict "The falsification gate", and the check
  is named rather than asserted. The gate's sentence is one-directional: *a
  count of zero means the test is decorative and the claim is unpinned*. It
  never asserts the converse, so the new rule's claim — that a non-zero count
  can also be unpinned — denies nothing the gate says, and the rule states the
  disjointness itself: "The gate above does not reach this — it asks what a
  wrong implementation would redden, and here one does". "A zero wearing a
  number" is a judgement about what the count is worth, not a claim that the
  recorded integer is zero, and the clause says so — "nothing was written down
  as zero". The two agree about what a zero means and the gate had no position
  on what a non-zero means, so there is nothing to contradict. The one residual
  ambiguity the reviewer found — which integer reaches the Falsification
  section when the rival reddens an unreachable path — is closed in the round:
  the count is recorded as it ran, with the unreachable path named beside it,
  so §6's "a count of zero is reported as a zero" keeps its referent.
- [x] AC5: `standard`, one independent pass, closing on it, and the tier was
  not raised. The pass ran against 3bf3f62 by an agent that did not perform
  the work and did not receive the executor's reasoning. It returned six
  must-fixes over eight findings; all six are repaired at de01d1a.

### Falsification
The ticket states the honest difficulty rather than discovering it: this is a
prose rule in a documentation repository and there is no suite for a sentence
to redden. N/A for a red count. What the ticket asks instead is done above —
the rule is applied to the four instances with the "no" recorded, and checked
against the gate for contradiction with the check named.

Per criterion, what a reader does differently: an executor writing a check
that asserts something of every member of a population asks what fixes that
population, and derives it or says in the docstring why it could not — instead
of writing the list and recording a non-zero count that the list makes true.

For the must-fixes repaired, per the contributor policy's §6:

- R1.1, R1.2, R1.3 and R1.5 — class: **which sentences of this rule state an
  obligation whose reach is not stated?** The headline is the instance. The
  question was asked of every sentence in the added text that binds a
  contributor. Siblings, each checked:
  - **The headline** — the instance. It bound any test asserting something of
    every member of a population, including a parametrised table of boundary
    inputs whose population the author is entitled to choose. Repaired: a
    "Which claims this reaches" paragraph asks what *fixes* the population, and
    a "What this does not reach" sentence names the cases outside it — the form
    "A number determined elsewhere has one site that goes red" already uses.
  - **The reachable-path clause** — same defect. It sat under the gate
    unqualified and so bound every rival, including a direct unit test of an
    internal helper called with an input no external caller can construct,
    which is the point of unit-testing a helper. Repaired: scoped to a claim
    about caller-visible behaviour, and pointed at "A test pins a claim, not a
    mechanism" for a claim whose subject is the unit.
  - **Tier 3** — same defect twice. It required the docstring statement to be
    "itself pinned", cross-referencing a shape the gate does not have — the
    gate's non-discriminating form is a docstring *label*, expressly not
    pinned, so tier 3 had no achievable remedy and the ticket's own example of
    tier 3 done right would have failed it. And it required nothing of the
    author's claim that tiers 1 and 2 were impossible, so the escape
    OMN-020-002's executor took was still open. Repaired on both counts.
  - **The binds-after-it sentence** — same question, reported as R1.7: silent
    on whether editing a listed check brings it under the rule, so a routine
    widening of an existing tuple might have owed a full derivation, which is
    the sweep the sentence disclaims arriving one file at a time. Repaired:
    editing does not bring it under; writing or rewriting the claim does.
  - **Tiers 1 and 2** — checked and sound. Each states a method, not an
    obligation of its own, and neither reaches beyond the population the
    headline's reach test now bounds.
  What a reader does differently: a contributor writing a table-driven test of
  eight boundary inputs reads the reach test, finds the test fixes its own
  population, and owes nothing — instead of owing a derivation or a docstring
  for a claim they never made.
- R1.4 — class: **which obligations in the added text lack a falsifier that can
  retire them?** The reachable-path clause is the instance. Asked of every
  bolded obligation added. Siblings: the headline and the tiers are retired by
  the two arms already written, both of which speak of derived populations; the
  reachable-path clause is about reachability and not about populations at all,
  so neither arm could ever retire it. Repaired: it has its own arm, on its own
  evidence. The reach paragraph states no obligation and needs none.
  What a reader does differently: a reviewer asking what would retire the
  reachable-path sentence finds an answer, rather than a rule that can only
  grow — which is the thing "Retiring a control" exists to prevent.
- R1.6 — note, repaired in the round and recorded under R1.1's class.

### Out of scope (per ticket)
Confirmed; nothing exceeds it.
- Any change to the falsification gate's own text — none. `git diff main...HEAD
  -- docs/quality-gates.md | grep -c '^-[^-]'` returns 0: the change is purely
  additive and no existing line in that file is altered or removed.
- Sweeping OMNISSIAH's existing tests — not done, and the rule states its own
  non-retrospectivity.
- The review-debt observation — absent from the diff.

### How to verify
1. `sed -n '/^\*\*An exhaustive claim is derived/,/doing the work claimed for it\./p' docs/quality-gates.md`
   — the rule as it stands.
2. `grep -c '^## ' docs/quality-gates.md` — 9, unchanged, which is why no index
   or map edit was owed.
3. `git diff main...HEAD -- docs/quality-gates.md | grep -c '^-[^-]'` — 0, which
   is the Out-of-scope check on the gate's own text.
4. Take each of the four instances in Context and run the rule's own words over
   it; the answers should be the AC2 table's, including the "no".

### Risks / follow-ups
- **The rule's name does not cover its fourth instance.** OMN-038 is caught by
  the reachable-path clause and not by the headline, so a rule titled "An
  exhaustive claim is derived, not listed" carries a sentence about something
  else. It is kept together because the two failures were found in one wave and
  share a cause — a count that looks like evidence and is not — and because the
  gate is where both belong. If the reachable-path clause is ever cited without
  the headline, that is the signal it should be its own rule.
- **Recorded, not repaired.** The ticket's Out of scope gives, as its reason
  for leaving out the review-debt observation, that "One day, four instances,
  all in one project … does not meet the second-instance bar". The bar's words
  are "in a second ticket **or** on a second project" — a disjunction — so one
  project is not disqualifying, and that reasoning would have disqualified
  EM-026 itself. The item is correctly left out on other grounds; only the
  stated reason is wrong, and it is in the ticket's prose rather than in any
  document this change touches. A later reader of that ticket should not take
  it as a reading of the bar.
- The second-instance bar is cleared for this rule on the bar's exact words:
  four instances in four tickets — OMN-024, OMN-034, OMN-020-002, OMN-038 —
  each named in Context with its round or its acceptance criterion, which is
  what "a name a reader cannot open is still a name, quoted with its round or
  its cost" asks.

### Review
One independent review pass, per "The operative test" for a change to a
process document. No second pass is taken.

| Round | Must-fix | Where (rules / lists / documents / tests) | Inside previous round's fix | Repaired by |
|---|---|---|---|---|
| 1 | 6 (of 8 findings) | documents: the headline bound any test asserting something of every member of a listed population, catching the ordinary table-driven test, with no reach test and no what-this-does-not-reach (must-fix, second column); the reachable-path clause sat unqualified under the gate and bound every rival, including a unit test of an internal helper (must-fix, second column); tier 3 required a docstring statement to be "itself pinned", a shape the gate does not have, leaving the escape hatch with no achievable remedy (must-fix, second column); tier 3 let the author self-certify that tiers 1 and 2 were impossible, which is the escape OMN-020-002's executor took (must-fix); the reachable-path clause had no falsifier, both arms speaking only of derived populations (must-fix); the rule was silent on which integer reaches the Falsification section; the binds-after-it sentence was silent on the edit case; AC3's literal words name two paths where the lifecycle requires three | — | de01d1a |

Derived from the row and not asserted beside it: six must-fixes over one review
round, all repaired. Round 1 has no round before it, so its inside-previous-fix
cell reads `—` and no line is uncountable.

- R1.1 · refuses · must-fix · `docs/quality-gates.md`, the rule's headline, against the form used by "A number determined elsewhere has one site that goes red", which carries both a reach question and a "what this section does not reach" · the headline bound any test asserting something of every member of a population the author listed, so a parametrised table of eight boundary inputs owed a derivation or a tier-3 docstring — remedy: add the reach question in the house form and a what-this-does-not-reach sentence; cost, if the remedy tightens a control: none, it narrows; inside previous fix: —
- R1.2 · refuses · must-fix · `docs/quality-gates.md`, "A rival must redden a path a caller can take" · unqualified and placed under the gate, it bound every rival, so every direct unit test of an internal helper recorded "a zero wearing a number" and owed a named reachable caller — remedy: scope it to a claim about caller-visible behaviour and route a claim about the unit to "A test pins a claim, not a mechanism"; cost, if the remedy tightens a control: none, it narrows; inside previous fix: —
- R1.3 · refuses · must-fix · `docs/quality-gates.md`, tier 3, "and that statement is itself pinned — the shape this gate already uses for a non-discriminating test" · the cross-reference is false: the gate's non-discriminating shape is a docstring label, expressly not pinned, so the escape hatch for cases where tiers 1 and 2 are impossible had no achievable remedy, and the ticket's own example of tier 3 done right would have failed it — remedy: state the gate's actual form; cost, if the remedy tightens a control: none, it loosens; inside previous fix: —
- R1.4 · permits · must-fix · `docs/tier-review-model.md`, "Retiring a control", "Every rule states its falsifier" · both arms of the Retired-when spoke only of derived populations, and neither could ever retire the reachable-path clause, which is about reachability — remedy: give that clause its own arm; cost, if the remedy tightens a control: none; inside previous fix: —
- R1.5 · permits · must-fix · `docs/quality-gates.md`, tier 3 · the rule required nothing of the author's claim that tiers 1 and 2 were impossible, so a written list survived with a docstring beside it — which is what OMN-020-002's executor did while tier 1 was available all along — remedy: tier 3 states why the first two were unavailable, in the same place; cost, if the remedy tightens a control: every honest tier-3 check pays one further sentence in its docstring; inside previous fix: —
- R1.6 · permits · note · `docs/quality-gates.md`, the reachable-path clause, against the gate's step 3 and §6's "A count of zero is reported as a zero" · the rule did not say which integer the executor writes when the rival reddens an unreachable path, so two executors record the same situation differently and neither is refutable — remedy: the count is recorded as it ran, with the unreachable path named beside it; cost: none; inside previous fix: —
- R1.7 · refuses · note · `docs/quality-gates.md`, "This binds checks written after it" · silent on the edit case, so a routine widening of an existing enumeration might owe a full derivation — the disclaimed sweep arriving one file at a time — remedy: say which it is; cost, if the remedy tightens a control: none as resolved, since editing does not bring a check under the rule; inside previous fix: —
- R1.8 · unranked · AC3's wording · the branch diff names three paths where the criterion names two, the third being the board row the lifecycle requires — remedy: the description names it and why; cost: none; inside previous fix: —

Both columns carry findings, and the second column carries three of the six
must-fixes. That is the result worth recording about this pass: a new rule
binding every future contributor was over-tight in three separate places —
catching ordinary table-driven tests, catching ordinary unit tests of helpers,
and leaving its own escape hatch unreachable — and none of the three was
visible to the executor who wrote it.

### Definition of Done (all tiers)
The four machine checks do not apply to a repository that publishes documents
and runs no suite; the falsification gate is discharged above in the form the
ticket's own Falsification section specifies, with the four instances worked
and the "no" recorded. Every measured figure names its baseline in the same
sentence and is read from the command named beside it. The independent pass a
process-document change takes has run and is recorded.
