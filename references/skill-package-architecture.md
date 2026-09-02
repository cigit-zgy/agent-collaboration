# Skill package architecture

This reference defines the standard architecture for reusable Agent Skills maintained
under the collaboration workflow. It deliberately separates three different
boundaries that must not be conflated:

```text
maintained source repository
portable Skill distribution bundle
embedded sub-Skill inside a larger project/repository
```

A Skill is a bounded capability package: it teaches an Agent when the capability
applies, how to perform the workflow, what supporting knowledge or deterministic
operations are available, and when the workflow is complete or must stop.

## 1. Portable Skill distribution bundle

The portable runtime package follows the common Agent Skills pattern:

```text
<skill-name>/
├── SKILL.md              # required Agent-facing entry
├── references/           # optional on-demand knowledge/contracts
├── scripts/              # optional deterministic executable helpers
└── assets/               # optional templates/static resources
```

Only `SKILL.md` is structurally required by this policy. Optional paths exist only
when the capability has a real consumer for them. Do not create empty directories to
make a Skill look complete.

`AGENTS.md` is not a required portable Skill runtime file. It belongs to repository
maintenance when a Skill is maintained as an independent source repository.

## 2. Maintained first-party Skill source repository

A standalone first-party Skill that is developed and maintained over time uses a
repository-level constitution in addition to its runtime Skill entry:

```text
<first-party-skill-repo>/
├── AGENTS.md             # required repository-maintenance constitution
├── SKILL.md              # required Agent-facing Skill entry
├── references/           # optional
├── scripts/              # optional
├── assets/               # optional
├── tests/                # optional first-party executable verification
├── pyproject.toml        # optional independent Python runtime/tooling authority
└── README.md             # optional human-facing repository documentation
```

`AGENTS.md` persists across the maintenance lifecycle. Skill maturity is not a reason
to delete it. It governs how future Agents should understand, modify, verify, and
maintain the source repository. It does not replace `SKILL.md`, and a portable Skill
packaging/install process may omit it when only runtime Skill resources are needed.

Use `skill-agents-template.md` when creating or normalizing this repository-level
constitution.

## 3. Embedded sub-Skill

A Skill embedded inside a larger project or composite repository normally inherits
the nearest applicable parent `AGENTS.md`:

```text
<project>/
├── AGENTS.md
├── SKILL.md
└── <sub-skill>/
    └── SKILL.md
```

Do not add one `AGENTS.md` per sub-Skill merely for symmetry. Add a nested
`AGENTS.md` only when that subtree has genuine maintenance rules that differ from the
parent scope and need narrower precedence.

## Core design rule

Use the smallest architecture that protects the real capability and maintenance
boundary.

```text
AGENTS.md
= repository maintenance/governance for a maintained source repository

SKILL.md
= activation + workflow + routing for Skill operation

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

A Skill must not acquire a file or directory merely because another Skill has it.

## `AGENTS.md` — repository-maintenance layer

For a maintained standalone first-party Skill repository, root `AGENTS.md` is
required by this first-party collaboration policy.

It should define only durable maintenance concerns such as:

- what repository is being maintained;
- which file is the Agent-facing Skill authority;
- source-repository versus distribution boundary;
- directory ownership;
- runtime/verification authority when relevant;
- maintenance invariants and non-goals;
- collaboration routing.

It must not duplicate the full runtime workflow from `SKILL.md`.

`AGENTS.md` is not required for a portable distribution bundle and is normally not
added to embedded sub-Skills that already inherit a parent constitution.

## `SKILL.md` — required runtime entry

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
Scripts must have a real workflow consumer.

## `assets/` — optional

Create `assets/` only for resources consumed by the Skill but not primarily read as
instructions.

Examples:

- document or figure templates;
- style files;
- static configuration fragments;
- reusable example input/output fixtures;
- icons or other generation resources.

Do not put explanatory Markdown in `assets/` when it is actually Agent reference
material; use `references/` instead.

## `tests/` — optional first-party extension

Create `tests/` when the maintained source repository owns executable behavior whose
contract warrants independent verification.

Tests should protect real Skill behavior, especially deterministic scripts, public
entry behavior, parsing/validation contracts, stable artifact shapes, and integration
boundaries that are easy to regress.

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

Purpose profile controls the Skill capability/package shape. It does not determine
whether `AGENTS.md` exists; maintenance ownership determines that separately.

### Documentation Skill

Use when the capability is primarily durable guidance, standards, or reasoning
instructions.

Portable package:

```text
<skill>/
├── SKILL.md
└── references/           # only if needed
```

A standalone maintained first-party repository adds root `AGENTS.md`.

### Executable Skill

Use when the capability combines Agent instructions with deterministic code.

Portable/source resources may include:

```text
<skill>/
├── SKILL.md
├── references/           # if domain/contracts are needed
├── scripts/
├── tests/                # source-repository verification only when warranted
└── pyproject.toml        # only if the Skill owns an independent runtime
```

A standalone maintained first-party repository adds root `AGENTS.md`.

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

Tests and runtime declarations remain conditional. A standalone maintained
first-party repository adds root `AGENTS.md`.

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

The standalone maintained repository has one root `AGENTS.md`; its embedded
sub-Skills normally do not each add another one. A project-level composite workflow
uses the dedicated `project-skill-template.md`.

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
loading the others. Do not split merely to make directories smaller.

## Progressive disclosure

Use this loading model for Skill operation:

```text
Skill discovery
→ read YAML name/description
→ activate Skill
→ read SKILL.md
→ read only the relevant reference/script/asset route
→ execute only what the active branch requires
```

Repository-maintenance Agents additionally read the applicable `AGENTS.md` before
modifying the source repository.

## Initialization decision

For a new standalone first-party Skill repository:

```text
1. Define ownership and capability boundary.
2. Create root AGENTS.md from skill-agents-template.md.
3. Choose the purpose profile.
4. Create SKILL.md from the matching purpose template.
5. Add references only for real on-demand knowledge.
6. Add scripts only for real deterministic operations.
7. Add assets only for real reusable resources.
8. Add tests only for executable behavior that needs verification.
9. Add pyproject.toml only if the Skill truly owns an independent Python runtime.
10. Add README.md only for a real human-facing repository need.
```

For an embedded sub-Skill, normally skip step 2 and inherit the parent `AGENTS.md`.
Never scaffold optional directories pre-emptively.

## Distribution rule

Do not equate Git repository contents with the portable Skill artifact.

A maintained source repository may contain:

```text
AGENTS.md
reports/
tests/
README.md
CI/configuration
other maintenance assets
```

that are not required for Skill runtime. Packaging or installation should include
only the resources needed by the Skill's operational contract. Do not delete
maintenance assets from source merely because they are excluded from a distribution
bundle.

## Relationship to repository ownership

Repository ownership, first-party/third-party classification, naming, local location,
GitHub visibility, and rename rules are governed by
`skill-repository-policy.md`.

For a new first-party Skill, apply:

```text
skill-repository-policy.md
→ skill-agents-template.md for standalone maintained repositories
→ skill-package-architecture.md
→ purpose-specific Skill template
```
