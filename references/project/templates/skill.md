# Project workflow SKILL.md template

Read `../../skill/writing.md` first. For behavior/design changes also read `../../skill/development.md`.

This template applies when a project exposes an Agent-operable multi-stage or composite workflow.

## Required information

A project workflow Skill communicates:

1. workflow purpose + activation condition;
2. minimum entry state;
3. top-level workflow/branch structure;
4. one owner for each top-level stage/capability;
5. stable input/output/progression gate for each route;
6. direct progressive-disclosure routing;
7. completion semantics.

These are information requirements, not mandatory headings.

## Context architecture

The workflow `SKILL.md` is the runtime index for that project capability.

```text
preferred
SKILL.md → owning stage/reference

avoid
SKILL.md → second index → owner
```

Name the primary owner directly for each route. Add a second owner only when the active concern genuinely requires both.

Do not instruct Agents to preload all sub-Skills/references or follow mandatory multi-reference chains.

Detailed stage contracts belong in their owners; the workflow Skill keeps only the selection information needed to reach them.

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
- Owner: <path/to/SKILL.md-or-reference>
- Also read: <NONE OR one genuinely required second owner>

## Completion
<Directly checkable terminal state.>

## Cold paths
<Templates/examples/history that are loaded only for the branch that needs them.>
````

When the project uses `design/`, identify the governing current `design_id`/topic without copying its design semantics into the Skill.

Do not treat `reports/concept/` as runtime authority. Concept notes are historical/exploratory input only.

Optional sections such as trust/lifecycle, runtime, human checkpoints, recovery, or STOP exist only when they change routing/execution.

## Development rule

A design-bearing workflow change follows:

```text
reports/concept/ exploration when useful
→ User + ChatGPT adjudication
→ current design/
→ workflow/stage SKILL.md + references
→ implementation
→ design-probing tests
```

Do not encode a new workflow semantic only in a concept note, FORMAL task, test fixture, or implementation patch.
