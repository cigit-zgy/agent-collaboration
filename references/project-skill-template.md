# Project workflow `SKILL.md` template

Use this template when a project exposes an Agent-operable multi-stage or composite
workflow. The Skill may live at any project-declared repository-relative path, such
as `<agent-name>/SKILL.md`; do not assume it must be at repository root.

The workflow Skill is not the project constitution. Root `AGENTS.md` owns
project-level governance and points to this Skill.

```markdown
---
name: <project-skill-name>
description: >
  <WHAT THIS WORKFLOW DOES>. Use when <CONCRETE TRIGGERING INTENTS OR INPUTS>.
---

# <Project Skill title>

## Role

This Skill is the project workflow router. It should let an unfamiliar Agent decide:

- whether the workflow applies;
- what input/state is required;
- which stage/capability owns the current task;
- what stable output that stage produces;
- what gate permits progression;
- which sub-Skill/reference to load next.

## When to use

Use this Skill when:

- <TRIGGER 1>;
- <TRIGGER 2>.

Do not use it for:

- <NON-GOAL 1>;
- <NON-GOAL 2>.

## Entry inputs / state

- `<INPUT_OR_STATE_1>`: <MEANING>;
- `<INPUT_OR_STATE_2>`: <MEANING>.

State only the entry gate needed to choose the correct route. Detailed schemas belong
in the owning sub-Skill/reference.

## Canonical workflow

```text
<stage_01>
→ <stage_02>
→ <stage_03>
```

or, for branching workflows:

```text
<input/state>
├── <condition A> → <capability A>
└── <condition B> → <capability B>
```

## Stage / capability routing

### `<stage_or_capability_a>`

- Purpose: <ONE-SENTENCE RESPONSIBILITY>.
- Required input: <MINIMUM STABLE INPUT>.
- Stable output: <OUTPUT/STATE>.
- Gate/next route: <DIRECTLY CHECKABLE CONDITION>.
- Owning Skill: `<path/to/sub-skill/SKILL.md>`.

### `<stage_or_capability_b>`

- Purpose: <ONE-SENTENCE RESPONSIBILITY>.
- Required input: <MINIMUM STABLE INPUT>.
- Stable output: <OUTPUT/STATE>.
- Gate/next route: <DIRECTLY CHECKABLE CONDITION>.
- Owning Skill: `<path/to/sub-skill/SKILL.md>`.

<Repeat only for real top-level routes.>

## Trust / lifecycle routing

<OPTIONAL. Include only when trust/lifecycle states affect eligibility or routing.>

```text
<state_01> → <state_02> → <state_03>
```

Explain only routing consequences. Detailed semantics belong in the owning project
contract/Skill.

## Progressive disclosure

Normal runtime path:

```text
applicable AGENTS.md
→ this SKILL.md
→ one owning sub-Skill
→ only references/scripts required by the active branch
```

Do not preload all sub-Skills, project concepts, references, scripts, tests, or
assets. Read project concept history only when a task genuinely needs design
rationale or supersession context.

## Runtime entry

<Declare only project-specific runtime identity/checks needed by this workflow.>

Example:

```text
Environment: <ENVIRONMENT_NAME>
Dependency/tooling authority: <pyproject.toml | other contract>
```

## Completion and stop conditions

Stop rather than guess when:

- no defined route matches the task;
- the owning sub-Skill/required contract is absent;
- an upstream gate is unsatisfied;
- required source/input authority is missing;
- a human/trust-state transition is required but not authorized.

The workflow completes only when the requested terminal output/state exists and its
route-level gates have passed.

## Boundaries

- This Skill owns routing, not detailed stage algorithms.
- Root `AGENTS.md` owns project governance.
- Branch-specific rules belong to the owning sub-Skill/reference.
- Do not create forwarding layers that add no real routing/contract value.
```

## Writing rules

For each top-level route, keep only five facts:

```text
purpose
required input
stable output
gate/next route
owning Skill
```

A project may expose this Skill to Codex under `$REPO_ROOT/.agents/skills/` when
repo-scoped auto-discovery is desired; see `skill-repository-policy.md`. Discovery
exposure is separate from the maintained source location.
