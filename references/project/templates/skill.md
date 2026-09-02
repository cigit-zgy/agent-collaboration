# Project workflow SKILL.md template

Read `../../skill/writing.md` first. This template applies when a project exposes an Agent-operable multi-stage or composite workflow.

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
