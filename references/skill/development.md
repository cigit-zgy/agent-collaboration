# Skill development lifecycle

This contract governs design, implementation, and testing of maintained first-party Skills.

## Core authority order

```text
reports/concept/ exploration/history when useful
→ User + ChatGPT adjudication
→ reports/design/ current authority
→ SKILL.md + references/
→ scripts/code/schema/config
→ tests/evaluation
→ runtime artifacts
```

For projects using the collaboration living-design model, current authority is the single `reports/design/` tree under `../project/design.md`; `reports/concept/` is history/input only.

Code and tests are projections/evidence. They do not independently define Skill behavior.

## Design-first boundary

When work changes or questions Skill capability semantics, routing, state, trust/provenance, recovery, completion, public API/schema meaning, scientific/product semantics, or cross-stage durable interfaces:

```text
observe problem / requirement
→ record concept history when useful
→ inspect reports/design/ + current Skill Markdown
→ determine DESIGN_GAP vs projection/implementation drift
→ if design: User + ChatGPT adjudicate
→ update reports/design/ coherently
→ project to SKILL.md/references
→ implement
→ test the resulting general contract
```

Do not begin by patching production code when intended behavior is not explicit in durable current design/Skill Markdown.

## Pure implementation drift

Repair code directly when intended behavior is already explicit and internally consistent in `reports/design/` + Skill Markdown, implementation clearly violates it, and no new semantic choice is required.

## Markdown before code

For design-bearing changes:

```text
reports/design/ updated/accepted
→ SKILL.md / references updated
→ committed task points to exact design + Markdown authority
→ Codex implements/repairs code to conform
```

A task is an execution specification, not the sole owner of new Skill semantics.

## No task-local patching

Do not add production behavior solely for one task/fixture/paper/repository/model/sample unless that behavior belongs to the accepted general Skill contract.

A concrete failure may reveal a general missing rule. Fix the rule at the `reports/design/`/Skill owner, not by mechanically generalizing the patch.

## Testing purpose

Skill tests primarily challenge whether the design/operational contract is sufficient, coherent, general, and implementable.

Prioritize representative normal flows, contract-implied boundaries, cross-stage invariants, failure/recovery, independent examples stressing generality, real artifacts when domain reality matters, and regressions for clarified general rules.

## Failure classification

```text
DESIGN_GAP
= reports/design/ does not determine adequate correct behavior
→ stop affected patching
→ User + ChatGPT adjudication
→ update reports/design/ if accepted

PROJECTION_DRIFT
= reports/design/ clear; Skill Markdown missing/inconsistent
→ fix Markdown first

IMPLEMENTATION_DRIFT
= reports/design/ + Skill Markdown clear; code violates them
→ repair code

TEST_DEFECT
= test demands behavior not required by accepted design
→ repair/remove test

ENVIRONMENT / TOOL DEFECT
= failure belongs to runtime/tool/external interface
→ repair at its owner
```

Codex reports the classification; it does not convert DESIGN_GAP into implementation drift just to finish.

## Prior art

For a new Skill, major capability, or substantial redesign, apply `../project/prior-art.md` when triggered before accepting custom design into `reports/design/`.

## Completion

Skill development is complete when any design-bearing change is durable in `reports/design/`, Skill Markdown faithfully projects it, implementation conforms without task-specific semantics, tests probe the general contract, and required verification/acceptance is complete.
