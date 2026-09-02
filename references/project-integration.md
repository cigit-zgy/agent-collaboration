# Project integration contract

This file is the current operational authority for connecting an individual project
repository to the global `agent-collaboration` workflow.

## Project entry

Each maintained project uses root `AGENTS.md` as its project constitution. It defines
project-specific authority, ownership, trust boundaries, collaboration linkage, the
declared design-authority model, and the Agent/workflow entry when one exists.

Do not copy global collaboration mechanics, verification levels, report templates, or
Git synchronization procedure into every project `AGENTS.md`.

Use:

- `project-architecture.md` for the canonical water-research repository
  responsibilities and initialization rules;
- `project-agents-template.md` to author/normalize root `AGENTS.md`;
- `project-skill-template.md` only when the project exposes an Agent-operable
  workflow;
- `report-concept-policy.md` to declare whether project concepts are canonical design
  specifications or decision-history assets.

## Design authority versus operational projection

A maintained scientific/research project may use `reports/concept/` as the canonical
User + ChatGPT design specification for project-level scientific, architectural,
trust, interface, and cross-stage decisions. The project must declare this explicitly
in root `AGENTS.md` and its concept index.

When declared:

```text
reports/concept/
= canonical design specification (WHAT + WHY)

project workflow/sub-Skills + references/
= operational projection of that design

scripts/code/schemas
= implementation

tests/
= conformance verification
```

Operational projections exist to make the accepted design executable by an Agent;
they do not gain authority to redefine the design. If projection or implementation
disagrees with a governing design concept, treat the difference as drift unless User
+ ChatGPT explicitly approve and update the design first.

This design authority remains separate from source-grounded scientific facts. A
project concept may define how source evidence is represented or validated, but the
registered scientific source/provenance chain owns model-specific scientific facts.

Projects that do not declare design-authority concepts may use `reports/concept/`
only as decision history/rationale, following `report-concept-policy.md`.

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

## Two reading modes

### Normal runtime

Routine project operation stays short:

```text
applicable project AGENTS.md
→ declared workflow SKILL.md
→ owning sub-Skill
→ only references/scripts required by the active branch
```

A design-authority concept does not need to be loaded on every run when its current
operational projection already exists.

### Design, redesign, or conformance audit

When the task changes architecture/scientific semantics, audits implementation
against the accepted plan, or investigates suspected drift:

```text
project AGENTS.md
→ reports/concept/README.md
→ only relevant design-authority concept topic(s)
→ affected workflow/stage SKILL and references
→ implementation/tests as needed
```

This is the correct path for rebuilding or auditing a stage from User + ChatGPT's
accepted project design.

## Collaboration route

When the work requires User ↔ ChatGPT ↔ Codex coordination, the project `AGENTS.md`
links to the canonical collaboration source:

```text
cigit-zgy/agent-collaboration
/Users/wenv/Documents/skills/agent-collaboration/SKILL.md
```

ChatGPT uses `agent-collaboration/SKILL.md` to route to the minimum collaboration
reference. Codex also inherits its machine-wide `~/.codex/AGENTS.md` instructions.

## New-project onboarding

Use this order:

```text
User identifies project
→ ChatGPT reads project-architecture.md
→ ChatGPT inspects actual repository
→ User + ChatGPT settle project purpose/authority/ownership/design-authority model
→ ChatGPT authors AGENTS.md from project-agents-template.md
→ initialize only the minimum project assets defined by project-architecture.md
→ when project concepts are design-authoritative, record the accepted design before implementation projection
→ if an Agent-operable workflow exists, author its SKILL.md from project-skill-template.md
→ expose repo-scoped Skill discovery only when desired
→ Codex is delegated only for genuinely local discovery/runtime/state verification or implementation
```

Do not create a separate initialization policy file; initialization belongs to the
project architecture contract so ownership and creation triggers stay in one place.

## Project-owned collaboration assets

Stable paths:

```text
reports/concept/   design authority or decision history, as declared by the project
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
= project-local constitution + authority declaration

project reports/concept/* (when role=design_authority)
= canonical User + ChatGPT project design specification

project workflow/sub-Skills + references
= Agent-operational projection of the accepted design

project scripts/code/schemas
= implementation

project tests
= implementation/projection conformance evidence

project source evidence/provenance
= model-specific scientific fact authority

project reports/chatgpt/*
= immutable local-execution specifications

project reports/codex/*
= execution evidence
```

User + ChatGPT own project/workflow design. Codex executes committed specifications
and must not silently redefine project architecture, scientific/product meaning,
workflow semantics, trust boundaries, or a governing design-authority concept.