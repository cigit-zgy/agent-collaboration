# Asset-oriented Skill template

Use for a Skill whose main work is producing or manipulating artifacts with reusable
static resources, templates, style files, or generation assets.

Recommended package:

```text
<skill-name>/
├── SKILL.md
├── references/           # optional guidance/contracts
├── scripts/              # optional deterministic helpers
└── assets/
```

Add tests or a runtime declaration only when the actual executable behavior warrants
them.

Suggested `SKILL.md`:

```markdown
---
name: <skill-name>
description: >
  <What artifact this Skill creates or manipulates>. Use when <concrete triggering
  artifact request or input>.
---

# <Skill title>

## Purpose

<Define the artifact capability and expected deliverable.>

## When to use

Use this Skill when:

- <trigger 1>;
- <trigger 2>.

Do not use it for:

- <non-goal 1>;
- <non-goal 2>.

## Inputs

- `<input artifact/context>`: <meaning>;
- <required style/specification/state if any>.

## Workflow

1. <Inspect the requested artifact and constraints.>
2. <Select only the relevant references/assets.>
3. <Use deterministic helpers when they protect geometry, formatting, conversion,
   or reproducibility.>
4. <Generate or modify the artifact.>
5. <Verify the artifact against the declared output contract.>

## Asset routing

Use only the assets required for the active request:

- `<assets/template-a>` when <condition>;
- `<assets/style-b>` when <condition>.

Do not treat explanatory Markdown as an asset; place Agent-readable guidance under
`references/`.

## Progressive disclosure

Read only the reference material relevant to the selected artifact path.
Do not preload all templates, styles, examples, or sibling resources.

## Outputs

- `<artifact type/path>`: <stable meaning>;
- <supporting derivative, if applicable>.

## Verification

Check only artifact properties that matter to the contract: structure, rendering,
geometry, format, required content, or deterministic reproducibility as applicable.

## Completion criteria

The Skill completes when the requested artifact exists in the required form and the
applicable artifact checks pass.

## Stop conditions

Stop rather than invent when:

- required source content or style authority is missing;
- an asset/template is required but unavailable;
- a requested change would violate a protected project or scientific contract.

## Boundaries

- `assets/` stores reusable resources, not project history or instructions.
- Keep artifact-generation logic separate from unrelated project workflows.
- Do not create scripts or tests merely because other asset Skills have them.
```
