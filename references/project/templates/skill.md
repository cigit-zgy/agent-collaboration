# Project workflow SKILL.md template

Read `../../skill/writing.md` first. For behavior/design changes also read `../../skill/development.md`.

This template applies when a project exposes an Agent-operable multi-stage or composite workflow.

## Required information

A workflow Skill communicates purpose/trigger, minimum entry state, top-level workflow, one owner per stage/capability, stable I/O/progression gates, direct routing, and completion semantics.

## Context architecture

Prefer:

```text
SKILL.md → owning stage/reference
```

Avoid mandatory second-index chains. Add a second owner only when the active concern genuinely requires both.

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
<Templates/examples/history loaded only when needed.>
````

When the project uses living design, identify the governing `reports/design/` topic/`design_id` without copying its semantics into the Skill.

Do not treat `reports/concept/` as runtime authority.

## Development rule

```text
reports/concept/ exploration when useful
→ User + ChatGPT adjudication
→ reports/design/ current authority
→ workflow/stage SKILL.md + references
→ implementation
→ design-probing tests
```

Do not encode a new workflow semantic only in concept history, a task, test fixture, or implementation patch.
