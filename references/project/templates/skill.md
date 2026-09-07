# Project workflow SKILL.md template

Read `../../skill/writing.md` for Markdown quality. When maintaining or changing Skill behavior/implementation, also read `../../skill/development.md` first.

This template applies when a project exposes an Agent-operable multi-stage or composite workflow.

## Development authority

For a design-bearing Skill change, the maintained order is:

```text
governing project/Skill concept
→ project workflow SKILL.md + owning sub-Skill/references
→ implementation
→ tests/evaluation
```

A project workflow Skill is an operational projection of accepted design; it is not the place to invent semantics after code/test failures.

If testing exposes missing or ambiguous workflow semantics, return to the governing concept/design and update the Skill Markdown before implementation repair. Pure implementation drift may be repaired directly only when the existing design + Skill Markdown already determine behavior without interpretation.

## Required information

A project workflow Skill communicates:

1. workflow purpose and activation condition;
2. minimum entry state;
3. top-level workflow/branch structure;
4. one owner for each top-level stage/capability;
5. stable input, output, and progression gate for each route;
6. progressive-disclosure routing;
7. completion semantics.

These are information requirements, not mandatory headings.

## Common shape

````markdown
---
name: <project-skill-name>
description: >
  <CAPABILITY>. Use when <TRIGGER OR INPUT STATE>.
---

# <Project Skill title>

## Purpose
<Workflow responsibility and stable outcome.>

## Entry state
<Minimum state needed to route.>

## Workflow
```text
<stage_01> → <stage_02> → <stage_03>
```

## Routing
### <stage>
- Purpose: <one responsibility>
- Required input: <minimum stable input>
- Stable output: <state/artifact>
- Gate: <directly checkable condition>
- Owner: <path/to/SKILL.md>

## Completion
<Directly checkable terminal state.>

## References
<Only active-branch resources.>
````

When the project uses design-authority concepts, identify the governing concept without copying it into the Skill. Optional sections such as trust/lifecycle, runtime, human checkpoints, recovery, or STOP exist only when they change routing or execution.

## Test interpretation

Project Skill tests are evidence about the general workflow contract. They should probe representative flows, boundaries, stage handoffs, recovery/failure semantics, and previously clarified invariants.

Do not tune the workflow Skill or implementation around one task fixture. Classify a failure using `../../skill/development.md` before changing code.
