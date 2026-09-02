# Project integration contract

This file is the current operational authority for connecting an individual project
repository to the global `agent-collaboration` workflow.

## Project entry

Each maintained project uses root `AGENTS.md` as its project constitution. It defines
project-specific authority, ownership, trust boundaries, collaboration linkage, the
project design-authority model, and the Agent/workflow entry when one exists.

Do not copy global collaboration mechanics, verification levels, report templates, or
Git synchronization procedure into every project `AGENTS.md`.

Use:

- `project-architecture.md` for canonical water-research repository responsibilities;
- `project-agents-template.md` for root `AGENTS.md`;
- `project-skill-template.md` for an Agent-operable workflow;
- `report-concept-policy.md` for concept/report boundaries.

## Project concept authority

For maintained scientific/research projects, `reports/concept/` is the canonical User
+ ChatGPT design specification.

It records only the accepted solution. It is not a discussion log, implementation
journal, task tracker, test report, or runtime-state store.

The authority chain is:

```text
reports/concept/
= accepted project solution/design

workflow/sub-Skills + references/
= operational projection of that design

scripts/code/schemas
= implementation

tests/
= conformance verification

workspace/data/runtime artifacts
= produced or mutable state
```

Downstream artifacts must conform to the concept design. If a Skill/reference or code
implementation differs from the governing concept, treat that as projection or
implementation drift. Do not rewrite the concept merely to match current code.

A design changes only after User + ChatGPT agree on a new solution and update the
concept first. Implementation then follows the revised concept.

Project design authority remains separate from scientific fact authority. Concepts may
define how evidence is represented or validated, but registered source/evidence owns
model-specific values, equations, symbols, and claims.

## Workflow Skill path

A project's canonical workflow Skill is project-declared; it need not live at
`project/SKILL.md`.

Typical multi-Skill water research project:

```text
<project>/
├── AGENTS.md
├── reports/concept/
└── <agent-name>/
    ├── SKILL.md
    ├── <capability-a>/SKILL.md
    └── <capability-b>/SKILL.md
```

If Codex repo-scoped Skill auto-discovery is desired, expose the maintained package
under `$REPO_ROOT/.agents/skills/` according to `skill-repository-policy.md`.

## Two reading modes

### Routine runtime

```text
project AGENTS.md
→ declared workflow SKILL.md
→ owning sub-Skill
→ required reference/script
```

Routine execution may rely on the already-derived operational projection and need not
load the full concept corpus.

### Design, redesign, or conformance audit

```text
project AGENTS.md
→ reports/concept/README.md
→ relevant concept topic(s)
→ affected Skill/reference projection
→ implementation/tests as needed
```

This path is mandatory when designing/rebuilding a stage, changing scientific or
architectural semantics, or auditing whether implementation still matches the accepted
solution.

## Collaboration route

When User ↔ ChatGPT ↔ Codex coordination is needed, project `AGENTS.md` links to:

```text
cigit-zgy/agent-collaboration
/Users/wenv/Documents/skills/agent-collaboration/SKILL.md
```

ChatGPT uses the collaboration Skill for delegation/verification policy. Codex also
inherits its machine-wide `~/.codex/AGENTS.md` instructions.

## New-project onboarding

```text
User identifies project
→ ChatGPT inspects repository
→ User + ChatGPT define accepted project solution in reports/concept/
→ ChatGPT authors/normalizes AGENTS.md
→ project Skills/references project the accepted solution into Agent operation
→ code/scripts implement that projection
→ tests verify conformity
→ Codex is delegated only for genuinely local execution or verification
```

## Project-owned assets

```text
reports/concept/   accepted project solution/design only
reports/chatgpt/   committed Codex tasks
reports/codex/     Codex execution evidence
```

Do not move formal tasks/reports into calendar archives. Do not place project assets in
the global collaboration repository.

## Authority split

```text
agent-collaboration/references/*
= global collaboration/project/Skill operating contracts

project AGENTS.md
= project-local constitution and routing

project reports/concept/*
= canonical User + ChatGPT project solution/design

project workflow/sub-Skills + references
= operational projection of the accepted design

project scripts/code/schemas
= implementation

project tests
= conformance evidence

project registered source/evidence
= model-specific scientific fact authority
```

User + ChatGPT own project design. Codex implements committed specifications and must
not silently redefine the governing concept.