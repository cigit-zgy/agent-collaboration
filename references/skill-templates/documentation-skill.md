# Documentation Skill template

Use for a Skill whose main value is durable instructions, standards, conventions,
or reasoning guidance. Keep the package minimal.

Recommended package:

```text
<skill-name>/
├── SKILL.md
└── references/           # only when on-demand detail is genuinely needed
```

Suggested `SKILL.md`:

```markdown
---
name: <skill-name>
description: >
  <What guidance this Skill provides>. Use when <concrete triggering task or intent>.
---

# <Skill title>

## Purpose

<One short paragraph defining the capability and expected outcome.>

## When to use

Use this Skill when:

- <trigger 1>;
- <trigger 2>;
- <trigger 3>.

Do not use it for:

- <adjacent but out-of-scope work>;
- <another non-goal>.

## Inputs / context

<What information, artifact, or task context the Agent must have before applying the
guidance.>

## Guidance workflow

1. <Read/inspect the minimum required context.>
2. <Apply the governing rules or decision logic.>
3. <Use only the references required by the active branch.>
4. <Produce the requested output/decision.>
5. <Check the completion criteria below.>

## Progressive disclosure

Read only the references required for the active task:

- `<references/topic-a.md>` when <condition>;
- `<references/topic-b.md>` when <condition>.

Do not load every reference by default.

## Output

<Describe the stable form of the result: recommendation, edited artifact, review,
analysis, etc.>

## Completion criteria

The task is complete when:

- <criterion 1>;
- <criterion 2>.

## Stop conditions

Stop rather than infer when:

- required source/context is missing;
- the requested decision belongs to a human or another authority;
- the task falls outside this Skill's defined scope.

## Boundaries

- This Skill provides guidance; it does not own unrelated project architecture.
- Do not introduce deterministic scripts unless a real repeatable operation emerges.
- Do not duplicate project-level governance from `AGENTS.md`.
```

Add `references/` only when moving detail out of `SKILL.md` materially improves
progressive disclosure. Documentation Skills should not acquire `scripts/`, `tests/`,
or a runtime merely for symmetry.
