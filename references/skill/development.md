# Skill development lifecycle

This contract governs design, implementation, and testing of maintained first-party Skills.

## Core authority order — hard boundary

A Skill is developed from durable current design semantics downward:

```text
reports/concept/ design exploration/history when useful
→ User + ChatGPT adjudication
→ current project/Skill design authority
→ SKILL.md + references/
→ scripts/code/schema/config
→ tests/evaluation
→ runtime artifacts
```

For projects using the collaboration living-design model, current authority is the single `design/` tree under `../project/design.md`; `reports/concept/` is history/input only.

Code and tests are projections/evidence of the Skill design. They do not independently define Skill behavior.

When a Skill task exposes a capability-semantic, workflow, state, trust, routing, recovery, or completion-design problem, User + ChatGPT MUST resolve the design first and make the accepted current result durable in the governing design authority. ChatGPT then updates the owning `SKILL.md` / `references/*.md` projection before implementation is changed.

Codex implements and verifies the committed Markdown contract. Codex MUST NOT resolve a design deficiency by inventing task-local behavior in code.

## When design-first is mandatory

Use the design-first path when work changes or questions any of the following:

```text
Skill purpose or capability boundary
activation / routing semantics
input / output / stable-state contract
workflow stage ownership or ordering
scientific/product semantics
trust/provenance boundary
recovery / retry / promotion semantics
error classification / fail-closed behavior
completion condition
public API/schema/CLI behavior whose meaning is part of the Skill contract
cross-stage interface or durable artifact semantics
```

Normal path:

```text
observe problem / new requirement
→ record a concept note when the exploration is worth preserving
→ inspect current design + current Skill Markdown
→ determine whether the defect is design or implementation drift
→ if design: User + ChatGPT adjudicate
→ update current design/ into one coherent state
→ project design into SKILL.md/references
→ implement code to conform
→ test the resulting design
→ if tests expose a new design defect, return upstream
```

Do not begin by patching production code when intended behavior is not yet explicit in the durable current design/Skill contract.

## Pure implementation drift exception

Do not edit design merely for ceremony.

If all of the following are true:

```text
intended behavior is already explicit and internally consistent in current design/Skill Markdown
AND implementation clearly violates that existing contract
AND no new semantic choice is required
```

then repair implementation directly and add/adjust only the smallest contract-level regression evidence needed.

A bug report or failing example does not automatically prove this exception. First determine whether the existing contract truly resolves the case without interpretation.

## Markdown projection before code — hard boundary

For a design-bearing Skill change, ChatGPT must make the accepted current design and operational projection readable before Codex receives implementation work.

Preferred handoff state:

```text
current design updated/accepted
→ SKILL.md / references updated
→ task points Codex to exact committed design + Markdown authority
→ Codex modifies implementation to conform
```

The FORMAL task is an execution specification, not a substitute for the Skill contract. Task-specific prose MUST NOT become the only place where new Skill semantics exist.

Forbidden pattern:

```text
failing task/example
→ add task-specific branch/flag/special case in code
→ tests pass
→ current design/Skill Markdown remains unchanged or ambiguous
```

Required pattern:

```text
failing task/example
→ identify general design consequence
→ update current design and Skill contract when needed
→ implement the general rule once at the correct owner
→ verify representative cases
```

## No task-local patching

A maintained Skill MUST NOT accumulate code that exists only to make one current task, fixture, paper, repository, model, or sample pass unless that behavior is explicitly part of the accepted current Skill contract.

Reject or redesign implementation patterns such as:

```text
special-case one known filename/sample/task ID
condition behavior on a current test fixture without a contract reason
restore rejected legacy behavior only for one failing consumer
add hidden fallback semantics absent from Skill Markdown
encode User-chat wording directly into production branches
weaken validation because a current example fails
```

A concrete case may reveal a general missing rule. Generalize the design consequence at the design/Skill owner, not by generalizing the patch mechanically.

## Testing purpose — hard boundary

Skill testing exists primarily to challenge whether the **Skill design and operational contract are sufficient, coherent, general, and implementable**.

Tests are not a contest to make one task perfect.

The testing question is:

```text
Given the accepted current Skill design,
does representative execution expose missing, contradictory, over-specific,
non-generalizable, or unimplementable semantics?
```

A useful test suite therefore emphasizes:

```text
representative normal flows
boundary cases implied by the contract
cross-stage/interface invariants
failure/recovery behavior
independent examples that stress generality
real artifacts when domain reality matters
regressions for previously clarified general rules
```

It should not grow primarily by adding one fixture for every task incident.

## Failure classification during Skill testing

When a Skill test fails, classify the failure before changing code:

```text
DESIGN_GAP
= current design/contract does not determine correct behavior, or is scientifically/product-wise inadequate
→ stop implementation patching
→ return to User + ChatGPT adjudication
→ update design/ if a new solution is accepted

PROJECTION_DRIFT
= current design is clear but SKILL.md/reference projection is missing/inconsistent
→ fix Markdown projection first
→ then implementation

IMPLEMENTATION_DRIFT
= current design + Skill Markdown are clear and code violates them
→ repair code

TEST_DEFECT
= test encodes behavior not required by accepted design, or overfits a fixture/task
→ repair/remove test

ENVIRONMENT / TOOL DEFECT
= failure comes from runtime/tool/external interface rather than Skill semantics
→ repair adapter/environment handling at its owner; do not redefine design without evidence
```

Codex reports the classification and evidence. It does not silently convert a `DESIGN_GAP` into `IMPLEMENTATION_DRIFT` to finish the task.

## Generality criterion

A Skill change is not successful merely because the triggering task passes.

Acceptance asks:

```text
Does the new rule apply to the intended capability class?
Is the rule stated at the correct durable owner?
Would an unfamiliar Agent derive the same behavior without seeing the original task?
Do tests exercise the rule independently of the triggering example?
Did implementation remove rather than add sample-specific branching where possible?
```

When the answer is no, the work is not ready even if the original failing case is green.

## Relationship to concept history and prior art

`reports/concept/` may preserve the exploration that led to a Skill change, but it is not current authority.

For a new Skill, major new capability, or substantial redesign, use `../project/prior-art.md` before accepting a custom design when that gate applies. Strong external Skills/projects may provide design precedent, but the accepted first-party living design and Skill Markdown remain authoritative.

## Relationship to writing and implementation standards

Use:

```text
writing.md
= how SKILL.md/references are written and owned

development.md
= current design → Markdown → implementation → design-probing-test lifecycle

../project/design.md
= living-design ownership + dynamic topic decomposition

../collaboration/implementation.md
= AI-assisted code quality, authorship, engineering discipline

../collaboration/verification.md
= verification level, evidence category, and placement
```

Do not duplicate those manuals here.

## FORMAL task requirement for Skill implementation

When FORMAL work changes a maintained first-party Skill's behavior or implementation, the committed task should identify:

```text
governing current design authority
exact committed SKILL.md / references that define intended behavior
whether the task is DESIGN_PROJECTION or IMPLEMENTATION_DRIFT
remaining local implementation/verification only
```

If Codex discovers a new design gap, it stops the affected code path and reports it for User + ChatGPT adjudication rather than expanding task semantics.

## Completion

Skill development is complete only when:

```text
any design-bearing change is durable in the current design authority
AND SKILL.md/references faithfully project that design
AND implementation conforms without task-specific semantic patches
AND tests probe the general contract rather than only the triggering task
AND discovered design gaps have been returned upstream rather than hidden in code
AND required verification/acceptance is complete
```
