# Skill package architecture

This reference defines the standard package architecture for a reusable Agent Skill.
It applies to first-party Skills designed or maintained under the collaboration
workflow. It is intentionally smaller than a general software or research-project
architecture.

A Skill is a bounded capability package: it teaches an Agent when the capability
applies, how to perform the workflow, what supporting knowledge or deterministic
operations are available, and when the workflow is complete or must stop.

## Canonical package

```text
<skill-name>/
├── SKILL.md              # required Agent-facing entry
├── references/           # optional on-demand knowledge/contracts
├── scripts/              # optional deterministic executable helpers
├── assets/               # optional templates/static resources
├── tests/                # optional first-party executable verification
├── pyproject.toml        # optional independent Python runtime/tooling authority
└── README.md             # optional human-facing documentation
```

Only `SKILL.md` is structurally required by this policy. Optional paths exist only
when the Skill has a real consumer for them. Do not create empty directories to make
a Skill look complete.

This package model is compatible with the common Agent Skills pattern of a required
`SKILL.md` plus optional `references/`, `scripts/`, and `assets/`. `tests/`,
`pyproject.toml`, and a human-facing `README.md` are first-party engineering
extensions and are not mandatory for portable Skill consumption.

## Core design rule

Use the smallest package that protects the capability boundary.

```text
SKILL.md
= activation + workflow + routing

references/
= knowledge the Agent may need, but should not preload

scripts/
= deterministic work that should not be reimplemented in free-form reasoning

assets/
= non-instruction resources consumed by the workflow

tests/
= verification of executable first-party behavior

pyproject.toml
= runtime/dependency authority only when the Skill truly owns one

README.md
= human-facing repository explanation, not Agent runtime instructions
```

A Skill must not acquire a directory merely because another Skill has it.

## `SKILL.md` — required

Every Skill has exactly one primary `SKILL.md` at its package root.

It must begin with YAML front matter containing at least:

```yaml
---
name: <skill-name>
description: >
  <what the capability does>. Use when <concrete triggering intents or inputs>.
---
```

The `description` is an activation surface, not a project abstract. It should let an
Agent decide whether to load the Skill before reading the full body.

The body should normally cover only the information required to operate the
capability:

- purpose/role;
- when to use and when not to use;
- required inputs or state;
- workflow or routing steps;
- stable outputs;
- progressive-disclosure routes;
- runtime/tools when relevant;
- completion criteria;
- stop conditions;
- boundaries/non-goals.

Detailed domain contracts, long examples, schemas, command catalogs, and reference
material should move out of `SKILL.md` when they are not needed for every invocation.

## `references/` — optional

Create `references/` only when the Skill has durable knowledge that should be loaded
on demand rather than kept in the root Skill.

Good contents include:

- domain or scientific contracts;
- field/schema semantics;
- standards and conventions;
- decision tables;
- workflow-specific instructions used only by one branch;
- long examples that teach behavior;
- external specification summaries or local indexes.

Rules:

- each reference should have a clear retrieval purpose;
- route references from `SKILL.md` or another directly relevant reference;
- prefer shallow navigation; do not build deep chains of references to references;
- add `references/README.md` only when the directory is large enough to need an
  index;
- do not use `references/` as a dumping ground for project history or transcripts.

## `scripts/` — optional

Create `scripts/` when deterministic code materially improves correctness,
repeatability, speed, or token efficiency.

Typical uses:

- parsing or normalization;
- format conversion;
- validation;
- deterministic extraction/materialization;
- repeatable file operations;
- small command-line helpers used directly by the Skill.

Do not create a script for work that is simpler and safer as one direct tool call or
one short Agent instruction. Do not move speculative abstractions into `scripts/`.

Scripts must have a real workflow consumer. Shared logic should not be extracted
until there are real consumers for the abstraction.

## `assets/` — optional

Create `assets/` only for resources consumed by the Skill but not primarily read as
instructions.

Examples:

- document or figure templates;
- style files;
- static configuration fragments;
- example input/output fixtures intended for reuse;
- icons or other generation resources.

Do not put explanatory Markdown in `assets/` when it is actually Agent reference
material; use `references/` instead.

## `tests/` — optional first-party extension

Create `tests/` when the Skill owns executable behavior whose contract warrants
independent verification.

Tests should protect real Skill behavior, especially:

- deterministic scripts;
- public command/entry behavior;
- parsing/validation contracts;
- stable artifact shapes;
- integration boundaries that are easy to regress.

Documentation-only Skills do not need tests merely for symmetry. Do not add
hash/freshness/duplicate tests unless a real persistent trust boundary requires them.

## `pyproject.toml` — optional runtime authority

A Skill may own `pyproject.toml` only when it independently owns executable Python
code and a real runtime/tooling contract.

Do not create one Python environment per Skill by default. Reuse a project-declared
runtime when the Skill exists inside a larger project and its code is part of that
project. Follow `skill-environment-policy.md` for environment ownership and rebuild
rules.

## `README.md` — optional human-facing documentation

Create a repository `README.md` when humans need installation, contribution,
maintenance, publication, or repository-level orientation that should not burden the
Agent-facing `SKILL.md`.

Do not duplicate the full Skill workflow in `README.md`. `SKILL.md` remains the
Agent-operational authority.

## Purpose profiles

Choose the package profile that matches the capability. Do not force all profiles
into one structure.

### Documentation Skill

Use when the capability is primarily durable guidance, standards, or reasoning
instructions.

```text
<skill>/
├── SKILL.md
└── references/           # only if needed
```

Typical examples: coding style, manuscript guidance, policy interpretation.

### Executable Skill

Use when the capability combines Agent instructions with deterministic code.

```text
<skill>/
├── SKILL.md
├── references/           # if domain/contracts are needed
├── scripts/
├── tests/                # when behavior warrants verification
└── pyproject.toml        # only if the Skill owns an independent runtime
```

Typical examples: workspace initialization, deterministic converters, validators.

### Asset-oriented Skill

Use when the capability generates or manipulates artifacts using reusable templates
or static resources.

```text
<skill>/
├── SKILL.md
├── references/           # if guidance is needed
├── scripts/              # if deterministic helpers are needed
└── assets/
```

Tests and runtime declarations remain conditional.

Typical examples: scientific figures, document templates, diagram generation.

### Composite/router Skill

Use when one Skill exists mainly to route an Agent across several bounded downstream
Skills or workflow branches.

```text
<composite-skill>/
├── SKILL.md
├── references/           # only cross-cutting routing contracts
└── <sub-skill-a>/
    └── SKILL.md
    ...
```

A composite Skill should stay thin. It owns activation, stage/branch routing, stable
interfaces, and stop conditions; downstream Skills own detailed procedures.

For a project-level composite workflow, prefer the dedicated
`project-skill-template.md` because a project root Skill also routes project concepts,
trust/lifecycle state, and project runtime identity.

## Skill boundary test

A Skill has a healthy boundary when the following are all reasonably clear:

1. one coherent capability or routing responsibility;
2. concrete activation conditions;
3. identifiable inputs/state;
4. identifiable stable outputs;
5. a completion or stop condition;
6. supporting resources that belong to this capability rather than the whole
   project.

Split a Skill when multiple branches have independent triggers, independent inputs
and outputs, distinct validation contracts, and can be operated or evolved without
loading the others.

Do not split merely to make directories smaller.

## Progressive disclosure

Use this loading model:

```text
Skill discovery
→ read YAML name/description
→ activate Skill
→ read SKILL.md
→ read only the relevant reference/script/asset route
→ execute only what the active branch requires
```

Do not preload every reference, script, asset, test, or sibling Skill.

## Initialization decision

When creating a Skill, decide in this order:

```text
1. Define the capability boundary and trigger.
2. Choose the purpose profile.
3. Create SKILL.md.
4. Add references only for real on-demand knowledge.
5. Add scripts only for real deterministic operations.
6. Add assets only for real reusable resources.
7. Add tests only for executable behavior that needs verification.
8. Add pyproject.toml only if the Skill truly owns an independent Python runtime.
9. Add README.md only for a real human-facing repository need.
```

Never scaffold optional directories pre-emptively.

## Relationship to repository ownership

This architecture describes the contents of a Skill package. Repository ownership,
first-party/third-party classification, naming, local location, GitHub visibility,
and rename rules are governed separately by `skill-repository-policy.md`.

For a new first-party Skill, apply both:

```text
skill-repository-policy.md
→ skill-package-architecture.md
→ purpose-specific Skill template
```
