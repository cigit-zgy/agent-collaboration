# Skill documentation writing standard

Load this reference when authoring or reviewing maintained `SKILL.md` files and their `references/` documentation.

## Governing model

```text
frontmatter description
= when this Skill should trigger

SKILL.md
= capability boundary + core workflow/routing + completion

references/
= bounded on-demand detail

scripts/
= deterministic reusable execution helpers
```

## Core principles

### Keep the trigger narrow

A Skill description should make clear what capability it provides and when to use it. Avoid long descriptions that enumerate many adjacent cases; large Skill catalogs compete for model context and make routing less reliable.

```yaml
---
name: <skill-name>
description: >
  <CAPABILITY>. Use when <CONCRETE TRIGGER>.
---
```

### Use progressive disclosure

Load only what the active task needs.

```text
Skill metadata
→ SKILL.md when triggered
→ one directly relevant reference/script when needed
```

Do not require Agents to preload an entire reference tree or historical material.

### Prefer goals and boundaries over itineraries

Describe:

```text
what outcome the Skill owns
what input/state it expects
what boundaries must hold
what completion looks like
where specialized detail lives
```

Avoid detailed step-by-step recipes for ordinary reasoning or engineering work when the model can choose the path safely. Specify exact procedures only when the sequence itself is part of correctness, safety, reproducibility, or an external interface contract.

### One concern, one owner

Every substantive rule has one owner. A router summarizes only enough to select that owner.

Do not duplicate project Design, task instructions, implementation policy, or historical rationale inside the Skill.

### Respect User priority

Generic Skill guidance does not override an explicit User instruction for the same scope. A Skill should stop work only at a real scientific/product, irreversible, permission, public/release, or explicitly declared checkpoint.

## `SKILL.md` should make recoverable

```text
purpose / capability boundary
trigger / entry state
core workflow or routing
true STOP / decision boundaries
completion state
specialized owner paths
```

These are information requirements, not mandatory headings.

For composite Skills, keep `SKILL.md` as a thin router. Name the primary owner directly for each route; avoid mandatory chains such as:

```text
SKILL.md → index → reference A → reference B
```

## References

Create a reference only when the topic is not needed on every invocation and has a real independent owner/consumer.

A reference should be self-contained for its concern and loaded on demand. Do not create miscellaneous containers such as `notes.md` or `general-guidance.md` merely to move prose out of `SKILL.md`.

## Scripts

Prefer a script when deterministic/repetitive execution is clearer and more reliable than repeatedly asking the model to reproduce the procedure.

Scripts do not become hidden design authority; they still conform to the Skill contract.

## Examples

Use examples only when they materially disambiguate a rule, mapping, output shape, or edge case. Examples illustrate the rule; they do not create hidden additional requirements.

## Scientific projects

Separate representation/operation rules from model-specific scientific facts:

```text
project Design / Skill reference
= how scientific information is represented, validated, or operated on

registered source/evidence
= source-specific values, equations, symbols, and scientific claims
```

## Review

A Skill architecture is healthy when:

```text
the description routes reliably
SKILL.md stays small enough to act as an entry point
specialized detail loads only when relevant
rules have single owners
routine work is not blocked by unnecessary approval pauses
completion is explicit
project-specific facts remain with their actual owners
```
