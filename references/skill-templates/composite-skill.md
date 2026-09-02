# Composite/router Skill template

Use for a Skill whose primary responsibility is routing an Agent across several
bounded downstream Skills or workflow branches.

Recommended package:

```text
<composite-skill>/
├── SKILL.md
├── references/           # only cross-cutting routing contracts
├── <sub-skill-a>/
│   └── SKILL.md
├── <sub-skill-b>/
│   └── SKILL.md
└── ...
```

A composite Skill should stay thin. Downstream Skills own detailed procedures.
For a project-level root workflow Skill, prefer `../project-skill-template.md`.

Suggested `SKILL.md`:

```markdown
---
name: <composite-skill-name>
description: >
  <What multi-stage or multi-branch capability this Skill routes>. Use when
  <concrete triggering workflow or family of tasks>.
---

# <Composite Skill title>

## Role

This Skill routes the active task to the correct downstream capability.
It owns activation, branch/stage selection, stable interfaces, and stop conditions.
It does not duplicate downstream implementation details.

## When to use

Use this Skill when:

- <trigger 1>;
- <trigger 2>.

Do not use it for:

- <work owned by a different top-level capability>.

## Entry inputs / state

<Describe only the shared entry state needed to choose the correct route.>

## Canonical routing

```text
<input/state>
→ <branch or stage A>
→ <branch or stage B>
→ ...
```

or:

```text
<input/state>
├── condition A → <sub-skill-a>
├── condition B → <sub-skill-b>
└── condition C → <sub-skill-c>
```

## Route table

### `<sub-skill-a>`

- Purpose: <one sentence>.
- Trigger/input: <routing condition>.
- Stable output: <output/state>.
- Gate/next route: <condition>.
- Owning Skill: `<sub-skill-a>/SKILL.md`.

### `<sub-skill-b>`

- Purpose: <one sentence>.
- Trigger/input: <routing condition>.
- Stable output: <output/state>.
- Gate/next route: <condition>.
- Owning Skill: `<sub-skill-b>/SKILL.md`.

<Repeat only for real downstream capabilities.>

## Progressive disclosure

Read only the one downstream Skill required by the active route. Do not preload all
sub-Skills or their references.

## Completion criteria

The composite workflow completes when the requested route reaches its declared
terminal output/state and all route-level gates have passed.

## Stop conditions

Stop rather than guess when:

- no defined route matches the current task;
- the required downstream Skill is absent;
- an upstream gate is not satisfied;
- the next route requires human authority or a trust-state transition not owned by
  this composite Skill.

## Boundaries

- This Skill owns routing, not downstream algorithms.
- Cross-cutting contracts may live in `references/`; branch-specific details belong
  to the owning sub-Skill.
- Do not create forwarding layers that add no real routing or contract value.
```
