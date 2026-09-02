# Project integration contract

This file is the current operational authority for connecting an individual project
repository to the global `agent-collaboration` workflow.

## Project entry

Each maintained project uses root `AGENTS.md` as its project constitution. It defines
project-specific authority, ownership, trust boundaries, collaboration linkage, and
the declared Agent/workflow entry when one exists.

Do not copy global collaboration mechanics, verification levels, report templates, or
Git synchronization procedure into every project `AGENTS.md`.

Use:

- `project-architecture.md` for the canonical water-research repository
  responsibilities and initialization rules;
- `project-agents-template.md` to author/normalize root `AGENTS.md`;
- `project-skill-template.md` only when the project exposes an Agent-operable
  workflow.

## Workflow Skill path

A project's canonical workflow Skill is project-declared. It does not have to live at
`project/SKILL.md`.

Typical multi-Skill water research project:

```text
<project>/
├── AGENTS.md
└── <agent-name>/
    ├── SKILL.md
    ├── <capability-a>/SKILL.md
    └── <capability-b>/SKILL.md
```

If Codex repo-scoped Skill auto-discovery is desired, expose the maintained package
under `$REPO_ROOT/.agents/skills/` according to `skill-repository-policy.md`. Do not
create a duplicate source tree merely for discovery.

## Normal runtime reading order

For project operation:

```text
applicable project AGENTS.md
→ declared workflow SKILL.md
→ owning sub-Skill
→ only references/scripts required by the active branch
```

This is intentionally shorter than the collaboration/design-history path.

Do not read project concepts by default. Read `reports/concept/README.md` and a
specific concept only when historical rationale, supersession, or a past design
choice is materially needed.

## Collaboration route

When the work requires User ↔ ChatGPT ↔ Codex coordination, the project `AGENTS.md`
links to the canonical collaboration source:

```text
cigit-zgy/agent-collaboration
/Users/wenv/Documents/skills/agent-collaboration/SKILL.md
```

ChatGPT uses `agent-collaboration/SKILL.md` to route to the minimum operational
reference. Codex also inherits its machine-wide `~/.codex/AGENTS.md` instructions.

## New-project onboarding

Use this order:

```text
User identifies project
→ ChatGPT reads project-architecture.md
→ ChatGPT inspects actual repository
→ User + ChatGPT settle project purpose/authority/ownership
→ ChatGPT authors AGENTS.md from project-agents-template.md
→ initialize only the minimum project assets defined by project-architecture.md
→ if an Agent-operable workflow exists, author its SKILL.md from project-skill-template.md
→ expose repo-scoped Skill discovery only when desired
→ Codex is delegated only for genuinely local discovery/runtime/state verification
```

Do not create a separate initialization policy file; initialization belongs to the
project architecture contract so ownership and creation triggers stay in one place.

## Project-owned collaboration assets

Stable paths:

```text
reports/concept/   decision history/rationale when needed
reports/chatgpt/   committed Codex tasks when issued
reports/codex/     Codex execution evidence when produced
```

Do not move formal task/report artifacts into weekly archives. Do not place project
assets in the global `agent-collaboration` repository.

## Authority split

```text
agent-collaboration/references/*
= current global collaboration/project/Skill contracts

project AGENTS.md
= project-local constitution

project workflow/sub-Skills
= current Agent-operational workflow contracts

project reports/concept/*
= accepted project decision history/rationale

project reports/chatgpt/*
= immutable local-execution specifications

project reports/codex/*
= execution evidence
```

User + ChatGPT own project/workflow design. Codex executes committed specifications
and must not silently redefine project architecture, scientific/product meaning,
workflow semantics, or trust boundaries.
