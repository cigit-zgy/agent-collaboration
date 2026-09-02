# Project workflow `SKILL.md` template

Use this template when a maintained project exposes an Agent-operable workflow. The
workflow Skill may live at repository root or, more commonly for a multi-Skill Agent
project, at a declared package path such as `<agent-name>/SKILL.md`.

The workflow Skill is the Agent-facing router for the project capability system. It
explains when the workflow applies, what entry state it expects, which stages or
branches exist, what each produces, which gate allows progression, and which
sub-Skill owns detailed procedure.

It is not the project constitution and must not duplicate root `AGENTS.md`, the global
collaboration protocol, or detailed sub-Skill manuals.

```markdown
---
name: <project-workflow-skill-name>
description: >
  <WHAT THIS WORKFLOW DOES>. Use when <TRIGGERING USER/AGENT INTENTS OR INPUTS>.
---

# <Project Workflow Skill Title>

## Role

This Skill is the Agent-facing project workflow/router.

It should let an unfamiliar Agent determine:

- whether this workflow applies;
- what input/state is required;
- which workflow stage or capability owns the current task;
- what stable output that stage must produce;
- what gate must pass before the next route;
- which downstream Skill/reference to read next.

Project governance remains in root `AGENTS.md`.

## When to use

Use this Skill when:

- <TRIGGER 1>;
- <TRIGGER 2>;
- <TRIGGER 3>.

Do not use it for:

- <CLEAR NON-GOAL OR ADJACENT WORKFLOW>;
- <ANOTHER NON-GOAL>.

## Inputs

Required entry inputs/state:

- `<INPUT_OR_STATE_1>`: <MEANING>;
- `<INPUT_OR_STATE_2>`: <MEANING>.

State any prerequisite gate explicitly. Do not repeat a full schema when an owning
contract/reference already defines it.

## Canonical workflow

```text
<stage_01>
→ <stage_02>
→ <stage_03>
→ ...
```

or, for branching capability systems:

```text
<input/state>
├── condition A → <capability-a>
├── condition B → <capability-b>
└── condition C → <capability-c>
```

Do not skip, merge, or invent canonical stages unless the project contract permits
it.

## Stage / capability routing

### 1. `<stage_or_capability_01>`

- Purpose: <ONE-SENTENCE RESPONSIBILITY>.
- Required input: <MINIMUM STABLE INPUT>.
- Stable output: <OUTPUT/STATE OWNED BY THIS STAGE>.
- Next-stage gate: <DIRECTLY CHECKABLE CONDITION>.
- Owning Skill: `<PATH/TO/SKILL.md>`.

### 2. `<stage_or_capability_02>`

- Purpose: <ONE-SENTENCE RESPONSIBILITY>.
- Required input: <MINIMUM STABLE INPUT>.
- Stable output: <OUTPUT/STATE OWNED BY THIS STAGE>.
- Next-stage gate: <DIRECTLY CHECKABLE CONDITION>.
- Owning Skill: `<PATH/TO/SKILL.md>`.

<REPEAT ONLY FOR REAL TOP-LEVEL ROUTES.>

## Trust or lifecycle progression

<OPTIONAL. Include only when meaningful project trust/lifecycle states exist.>

```text
<state_01>
→ <state_02>
→ <state_03>
```

Explain only what each state means for routing/eligibility. Detailed semantics belong
in project concepts/contracts.

## Progressive disclosure

```text
root AGENTS.md
→ project concept index when durable design context is needed
→ this workflow SKILL.md
→ the one owning downstream Skill
→ only references/scripts required by that Skill
```

Do not preload every concept, Skill, reference, script, asset, or test.

## Runtime entry

<State only project-specific runtime identity or entry checks.>

Example:

```text
Environment: <ENVIRONMENT_NAME>
Dependency/tooling authority: <pyproject.toml | package.json | other contract>
```

Do not copy global environment, Git, verification, or security-tool procedures from
`agent-collaboration`.

## Completion and stop conditions

Stop rather than guessing when:

- the owning downstream Skill or required contract is absent;
- the upstream stage gate is not satisfied;
- required source/input evidence is missing;
- a project-defined human decision is required;
- continuing would cross a trust/lifecycle boundary without the required promotion.

A workflow is complete only when the requested terminal output/state exists and all
required gates for that state have passed.

## Boundaries

- <PROJECT-SPECIFIC ROUTING INVARIANT>.
- <WHAT THIS WORKFLOW SKILL MUST NOT OWN>.
- <WHAT DOWNSTREAM SKILLS MUST NOT BYPASS>.
```

## Placement rule

Do not create both repository-root `SKILL.md` and `<agent-name>/SKILL.md` when they
would describe the same workflow. Choose one canonical workflow location and declare
it in root `AGENTS.md`.

For a coordinated collection of project Skills, prefer:

```text
<project>/
├── AGENTS.md
└── <agent-name>/
    ├── SKILL.md
    ├── <capability-a>/SKILL.md
    ├── <capability-b>/SKILL.md
    └── ...
```

The package root Skill stays thin; sub-Skills own detailed capability procedures.

## Writing rules

A good project workflow `SKILL.md` is compact and stable. For each top-level stage or
capability, prefer five routing facts:

```text
purpose
required input
stable output
next-stage gate
owning Skill
```

Move detailed schemas, scientific rules, repair logic, commands, validation
algorithms, and long examples to the owning sub-Skill/reference.

## Onboarding procedure

```text
User identifies project
→ ChatGPT reads agent-collaboration
→ ChatGPT reads project-architecture.md
→ ChatGPT establishes/normalizes root AGENTS.md
→ User + ChatGPT decide whether an Agent-operable workflow exists
→ choose the canonical workflow Skill path, normally <agent-name>/SKILL.md for a
  multi-Skill Agent project
→ instantiate this template
→ add sub-Skills only for real bounded capabilities
→ Codex is used only for genuinely local execution/discovery verification
```

Workflow design remains a User + ChatGPT responsibility. Codex executes committed,
implementation-ready tasks and must not silently redefine workflow semantics.

## Quality criteria

After reading the workflow Skill, an unfamiliar compatible Agent should be able to
answer:

1. When should this Skill activate?
2. What does the project workflow accomplish?
3. What entry inputs/state are required?
4. What are the top-level stages or capability routes?
5. What does each consume and produce?
6. What gate allows progression?
7. Which downstream Skill owns the current task?
8. What trust/lifecycle state is relevant, if any?
9. When must execution stop?
10. What project runtime identity applies?
