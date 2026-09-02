# Maintained first-party Skill repository `AGENTS.md` template

Use this template for a standalone first-party Skill repository that is expected to
be maintained over time. This file governs repository maintenance; it is not part of
the portable Skill runtime contract.

Do not add a nested `AGENTS.md` to every embedded sub-Skill. Embedded Skills normally
inherit the nearest applicable parent/project `AGENTS.md` unless they have genuine
local maintenance rules that require a narrower scope.

```markdown
# <SKILL_NAME> repository context

## Repository identity

This repository is the maintained first-party source repository for the
`<SKILL_NAME>` Skill.

<ONE-TO-THREE SENTENCES: what capability the Skill provides and why the repository
exists.>

## Authority and scope

User + ChatGPT own Skill design and maintenance decisions. Codex executes approved,
implementation-ready local tasks and must not silently redesign the capability.

Agent-facing Skill operation is defined by root `SKILL.md`. Repository-maintenance
rules belong here. Do not duplicate the full Skill workflow in `AGENTS.md`.

## Source repository versus distribution

This repository may contain maintenance assets that are not required in a portable
Skill distribution.

```text
maintained source repository
├── AGENTS.md
├── SKILL.md
├── <optional maintenance/runtime resources>
└── ...

portable Skill distribution
├── SKILL.md
├── references/   # when required for operation
├── scripts/      # when required for operation
└── assets/       # when required for operation
```

`AGENTS.md` persists for the lifetime of this maintained source repository. Do not
delete it merely because the Skill is mature. A packaging/install process may omit
it when the target is only the portable runtime Skill bundle.

## Repository ownership

```text
SKILL.md       Agent-facing activation/workflow authority
references/    <if present: on-demand knowledge/contracts>
scripts/       <if present: deterministic executable helpers>
assets/        <if present: reusable static resources/templates>
tests/         <if present: first-party executable verification>
pyproject.toml <if present: independent runtime/tooling authority>
README.md      <if present: human-facing repository documentation>
```

Remove lines for paths that do not exist. Do not create optional paths only to match
this template.

## Maintenance rules

- Keep `SKILL.md` focused on activation and operation.
- Put long/on-demand guidance in `references/`.
- Put deterministic repeatable operations in `scripts/` only when they have real
  consumers.
- Keep human-facing repository material out of the Agent runtime instructions when
  it is not needed for operation.
- Preserve one authoritative source for each rule or contract; route instead of
  duplicating.
- Follow the owning runtime/environment contract; do not create one environment per
  Skill by default.

## Runtime and verification

<STATE WHETHER THIS SKILL OWNS AN INDEPENDENT RUNTIME.>

Examples:

`No independent runtime; documentation-only Skill.`

or:

```text
Runtime authority: pyproject.toml
Environment: <name or project-owned runtime>
```

Use only verification warranted by actual executable behavior and the active task.
Global collaboration, Git synchronization, delegation, and verification-level rules
come from `cigit-zgy/agent-collaboration`.

## Distribution boundary

State which repository paths are required for Skill operation and which are
maintenance-only. Do not assume the entire Git repository is the portable Skill
artifact.

## Hard boundaries

- `AGENTS.md` governs repository maintenance; `SKILL.md` governs Skill operation.
- Do not delete `AGENTS.md` at maturity while the source repository remains actively
  maintained.
- Do not add nested `AGENTS.md` to embedded sub-Skills without genuine local rules.
- Do not normalize third-party Skills to this first-party template.
- Do not create optional directories, runtime files, or tests without real
  consumers.
```

## When not to use this template

Do not use this template for:

- a portable Skill bundle that is not itself a maintained source repository;
- an embedded sub-Skill that is already governed by a parent project/repository
  `AGENTS.md` and has no special local maintenance rules;
- a third-party Skill whose upstream repository controls its own instructions;
- a full scientific/software project; use the project-level `AGENTS.md` template
  instead.
