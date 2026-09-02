# Skill package architecture

This file is the current operational authority for the internal structure of a
reusable Skill and for deciding which optional resources belong to it.

## Three boundaries

Do not conflate:

```text
1. maintained source repository
2. Codex discovery exposure
3. portable runtime/distribution bundle
```

Repository/discovery placement is governed by `skill-repository-policy.md`. This file
only defines package contents and creation conditions.

## Minimal Skill package

```text
<skill-name>/
├── SKILL.md              # required Agent-facing capability entry
├── references/           # optional on-demand knowledge/contracts
├── scripts/              # optional deterministic helpers
├── assets/               # optional reusable non-instruction resources
├── tests/                # optional first-party executable verification
├── pyproject.toml        # optional independent Python runtime/tooling authority
└── README.md             # optional human-facing documentation
```

Only `SKILL.md` is required by this policy. Optional paths exist only when they have
a real owner, artifact, and consumer. Do not create empty directories for symmetry.

A maintained standalone first-party source repository additionally has root
`AGENTS.md`; that is a repository-maintenance asset, not a required portable Skill
runtime file.

## `SKILL.md`

Every Skill has one primary `SKILL.md` at the package root. It begins with at least:

```yaml
---
name: <skill-name>
description: >
  <what the capability does>. Use when <concrete trigger/input>.
---
```

`description` is the activation surface. The body should contain only information
needed to operate or route the capability:

- purpose/role;
- use/non-use triggers;
- required input/state;
- workflow or routing;
- stable outputs;
- completion and stop conditions;
- direct routes to required resources.

Move long contracts, schemas, standards, examples, and branch-specific detail to
`references/`.

## `references/`

Create only for durable knowledge that should be loaded on demand, for example:

- scientific/domain contracts;
- field/schema semantics;
- standards and conventions;
- decision tables;
- long branch-specific guidance.

Keep navigation shallow. Do not use `references/` for project history or transcripts.

## `scripts/`

Create only when deterministic code materially improves correctness, repeatability,
speed, or token efficiency. Typical consumers include parsing, normalization,
validation, conversion, and repeatable file operations.

Do not create scripts for work that is simpler and safer as one direct tool call or
one short instruction. Scripts require a real workflow consumer.

## `assets/`

Create only for reusable resources consumed by the Skill but not primarily read as
instructions, such as templates, style files, static configuration fragments, or
reusable fixtures.

Agent-readable explanatory Markdown belongs in `references/`, not `assets/`.

## `tests/`

Create only when executable first-party behavior warrants independent regression
protection. Documentation-only Skills do not need tests for symmetry.

## `pyproject.toml`

Create only when the Skill independently owns executable Python code and a real
runtime/tooling contract. Embedded Skills normally use the parent project's declared
runtime rather than creating one environment per Skill.

## `README.md`

Create when humans need repository-level orientation, installation, contribution, or
maintenance information that should not burden the Agent-facing `SKILL.md`.

## Purpose profiles

Choose the smallest real profile:

- **Documentation**: instructions/standards; usually `SKILL.md` plus optional
  `references/`.
- **Executable**: Agent guidance plus deterministic operations; may add `scripts/`,
  relevant tests, and runtime authority when independently owned.
- **Asset-oriented**: artifact creation/manipulation using reusable assets and
  optional deterministic helpers.
- **Composite/router**: routes across bounded downstream capabilities; stays thin and
  does not duplicate downstream procedures.

Use the corresponding scaffold under `skill-templates/`. A project-level workflow
Skill may instead use `project-skill-template.md`.

## Boundary test

A Skill boundary is healthy when these are clear:

1. coherent capability or routing responsibility;
2. concrete activation condition;
3. identifiable input/state;
4. identifiable stable output;
5. completion/stop condition;
6. supporting resources that belong to this capability rather than the whole
   project.

Split only when independent triggers, interfaces, and validation responsibilities
make separate capabilities real. Do not split merely to reduce directory size.

## Progressive disclosure

Runtime loading should remain short:

```text
name + description
→ SKILL.md
→ only resources required by the active branch
```

Project `AGENTS.md` may explicitly route to a Skill, and Codex may also discover a
Skill through `.agents/skills` locations. Do not insert concept/history documents
into normal Skill execution unless historical design context is actually needed.

## Creation sequence

```text
define capability boundary + trigger
→ choose purpose profile
→ create SKILL.md
→ add references/scripts/assets only for real consumers
→ add tests/runtime/README only when warranted
```

For standalone first-party repository ownership and discovery exposure, apply
`skill-repository-policy.md` and `skill-agents-template.md` in addition to this
package contract.
