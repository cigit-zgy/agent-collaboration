# Executable Skill template

Use for a Skill that combines Agent instructions with deterministic scripts,
commands, validators, converters, or other repeatable operations.

Recommended package:

```text
<skill-name>/
├── SKILL.md
├── references/           # optional
├── scripts/
├── tests/                # when executable behavior warrants verification
└── pyproject.toml        # only if the Skill owns an independent Python runtime
```

Suggested `SKILL.md`:

```markdown
---
name: <skill-name>
description: >
  <What executable capability this Skill provides>. Use when <concrete triggering
  input or operation>.
---

# <Skill title>

## Purpose

<Define the capability and stable result in one short paragraph.>

## When to use

Use this Skill when:

- <trigger 1>;
- <trigger 2>.

Do not use it for:

- <non-goal 1>;
- <non-goal 2>.

## Required inputs / state

- `<input 1>`: <meaning>;
- `<input 2>`: <meaning>.

State any prerequisite gate explicitly.

## Workflow

1. <Validate or inspect entry state.>
2. <Run the minimal deterministic operation or script.>
3. <Inspect the result needed for the active branch.>
4. <Apply Agent reasoning only where deterministic logic is insufficient.>
5. <Produce the stable output and verification evidence.>

## Deterministic operations

Use:

- `<scripts/tool-a.py>` for <real operation>;
- `<scripts/tool-b.py>` for <real operation>.

Do not reimplement these operations in free-form reasoning. Do not add scripts that
lack a real workflow consumer.

## Progressive disclosure

Read only the reference material required by the active operation:

- `<references/contract-a.md>` when <condition>;
- `<references/contract-b.md>` when <condition>.

## Outputs

- `<output/state>`: <stable meaning>;
- <diagnostic/report if applicable>.

## Runtime / tools

<Declare only Skill-specific runtime identity.>

If the Skill owns an independent Python runtime:

```text
Dependency/tooling authority: pyproject.toml
```

If the Skill is embedded in a larger project, use the project's declared runtime
instead of creating a separate environment.

## Verification

Run the smallest checks that directly protect this Skill's executable contract.
Detailed project/release verification comes from the owning project or collaboration
policy.

## Completion criteria

The Skill completes when:

- required deterministic operations succeed;
- the stable output satisfies its declared contract;
- no blocking diagnostic remains.

## Stop conditions

Stop rather than guess when:

- required input/state is missing;
- a deterministic operation fails in a way the contract does not resolve;
- required authority/human approval is missing;
- continuing would mutate an environment or trust boundary without authorization.

## Boundaries

- Keep scripts deterministic and scoped to this capability.
- Keep Agent interpretation separate from deterministic transformation.
- Do not create speculative shared abstractions or duplicate project-level runtime
  policy.
```

Use `tests/` only when there is executable behavior worth independently protecting.
Use `pyproject.toml` only when this Skill truly owns its runtime rather than borrowing
the parent project's runtime.
