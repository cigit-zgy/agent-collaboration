# Project root `SKILL.md` template

Use this template when a project repository needs a root workflow Skill. The root
Skill is the Agent-facing workflow/router for the project. It explains when the
project workflow applies, what inputs it expects, which stages exist, what each stage
produces, and which downstream Skill owns the detailed procedure.

The root Skill is not the project constitution and must not duplicate `AGENTS.md`,
the global collaboration protocol, or detailed sub-Skill manuals.

Follow the public Agent Skills pattern: `SKILL.md` begins with YAML front matter
containing a stable `name` and a trigger-oriented `description`; detailed material is
loaded progressively from downstream Skills and references only when needed.

Replace placeholders and remove sections that are genuinely not applicable.

```markdown
---
name: <project-skill-name>
description: >
  <WHAT THIS WORKFLOW DOES>. Use when <TRIGGERING USER/AGENT INTENTS OR INPUTS>.
---

# <Project Skill Title>

## Role

This is the project workflow router.

It should let an unfamiliar Agent determine:

- whether this Skill applies;
- what input/state is required;
- which workflow stage owns the current task;
- what stable output that stage must produce;
- what gate must pass before the next stage;
- which downstream Skill/reference to read next.

Do not duplicate project-governance rules from root `AGENTS.md` or detailed
implementation/scientific rules from downstream Skills.

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

State any entry gate that must already be satisfied. Do not repeat the full input
schema when an owning contract/reference already defines it.

## Canonical workflow

```text
<stage_01>
→ <stage_02>
→ <stage_03>
→ ...
```

Do not skip, merge, or invent stages unless the owning project contract explicitly
allows it.

## Stage routing

### 1. `<stage_01>`

- Purpose: <ONE-SENTENCE RESPONSIBILITY>.
- Required input: <MINIMUM STABLE INPUT>.
- Stable output: <OUTPUT/STATE OWNED BY THIS STAGE>.
- Next-stage gate: <DIRECTLY CHECKABLE CONDITION>.
- Owning Skill: `<PATH/TO/SKILL.md>`.

### 2. `<stage_02>`

- Purpose: <ONE-SENTENCE RESPONSIBILITY>.
- Required input: <MINIMUM STABLE INPUT>.
- Stable output: <OUTPUT/STATE OWNED BY THIS STAGE>.
- Next-stage gate: <DIRECTLY CHECKABLE CONDITION>.
- Owning Skill: `<PATH/TO/SKILL.md>`.

<REPEAT ONLY FOR REAL TOP-LEVEL STAGES.>

## Trust or lifecycle progression

<OPTIONAL. Include only when the project has meaningful trust/lifecycle states.>

```text
<state_01>
→ <state_02>
→ <state_03>
```

Explain only what each state means for routing or eligibility. Detailed semantics
belong in the owning project concept/contract.

## Progressive disclosure

For an active task, read only what is needed:

```text
root AGENTS.md
→ project concept index when durable design context is needed
→ this root SKILL.md
→ the owning downstream Skill
→ only references/scripts required by that downstream Skill
```

Do not preload every project concept, downstream Skill, reference, script, or test.

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

A workflow is complete only when the project-defined terminal output/state exists
and all required gates for that state have passed.

## Boundaries

- <PROJECT-SPECIFIC ROUTING INVARIANT>.
- <WHAT THIS ROOT SKILL MUST NOT OWN>.
- <WHAT DOWNSTREAM SKILLS MUST NOT BYPASS>.
```

## Writing rules

A good project root `SKILL.md` should be compact and stable. Prefer roughly 100–200
lines when practical; length is not a target by itself.

The `description` is especially important because Agents use it to decide whether to
activate the Skill. Describe concrete triggering intents and inputs rather than vague
phrases such as “help with this project.”

For each top-level stage, keep the root description to five routing facts:

```text
purpose
required input
stable output
next-stage gate
owning Skill
```

Move detailed schemas, scientific rules, repair logic, command sequences, validation
algorithms, and implementation instructions to the owning downstream Skill or
reference.

## Onboarding procedure

For a new project:

```text
User identifies the project
→ ChatGPT reads agent-collaboration
→ ChatGPT establishes/normalizes project AGENTS.md from project-agents-template.md
→ ChatGPT reads this project-skill-template.md
→ ChatGPT inspects the actual repository and existing workflows
→ User + ChatGPT settle the canonical workflow and stage boundaries
→ ChatGPT writes/commits the root SKILL.md when connected tools are sufficient
→ Codex is used only for genuinely local execution/discovery verification
```

The workflow design is a User + ChatGPT responsibility. Codex executes committed,
implementation-ready tasks and must not silently redesign project stage semantics.

## Quality criteria

An unfamiliar compatible Agent should be able to answer after reading the root
`SKILL.md`:

1. When should this Skill activate?
2. What does the project workflow accomplish?
3. What inputs/state are required to enter?
4. What are the real top-level stages and their order?
5. What does each stage consume and produce?
6. What gate allows progression?
7. Which downstream Skill owns the current stage?
8. What trust/lifecycle state is relevant, if any?
9. When must the Agent stop rather than infer?
10. What project runtime identity applies?

If the file starts functioning as a project constitution or as a detailed sub-Skill
manual, move that content to `AGENTS.md`, project concepts, or the owning downstream
Skill instead.