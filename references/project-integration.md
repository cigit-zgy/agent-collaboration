# Project integration contract

This reference defines how an individual project repository connects to the global
`agent-collaboration` protocol without moving project-specific work into the
`agent-collaboration` repository.

## Project entry point

Each maintained project repository uses its root `AGENTS.md` as the project-level
entry point and constitution. It is not a copy of the global collaboration protocol.

A project `AGENTS.md` should identify:

- project purpose and scope;
- project-specific scientific/product/architectural authorities;
- the canonical collaboration repository;
- the Codex local collaboration entry;
- the canonical project workflow `SKILL.md` path when one exists;
- the project concept/report locations;
- project-specific precedence, trust-state, runtime, and human-decision rules.

The project workflow Skill does **not** have to live at repository root. For a
multi-Skill Agent project, the normal pattern is:

```text
<project>/
├── AGENTS.md
└── <agent-name>/
    ├── SKILL.md
    ├── <capability-a>/SKILL.md
    └── <capability-b>/SKILL.md
```

Root `AGENTS.md` must declare the actual workflow path, for example
`water-bioprocess-agent/SKILL.md`.

Recommended collaboration block:

```markdown
## Collaboration protocol

Canonical collaboration repository:
`cigit-zgy/agent-collaboration`

Codex local entry:
`/Users/wenv/Documents/skills/agent-collaboration/SKILL.md`

Use the global collaboration protocol for User ↔ ChatGPT ↔ Codex workflow.
Project-specific scientific, product, architectural, and trust-state rules in this
repository remain authoritative for this project.
```

Do not copy detailed global verification levels, Git synchronization, report
templates, or delegation procedure into project `AGENTS.md`.

## Canonical project architecture

For water-domain mechanistic-model or Agent research repositories, use:

`references/project-architecture.md`

It defines responsibility slots and whether each path is required or conditional.
It is a responsibility map, not a command to create every directory.

## Project `AGENTS.md` template

The reusable constitution scaffold is:

`references/project-agents-template.md`

User + ChatGPT inspect the actual repository and instantiate only applicable durable
rules. Project-constitution design is not delegated to Codex merely because Codex can
edit local files.

## Project workflow `SKILL.md` template

The reusable Agent-facing workflow scaffold is:

`references/project-skill-template.md`

Use it only when the project exposes an Agent-operable workflow. The resulting Skill
may live at `<agent-name>/SKILL.md` or another explicitly declared project path.

It should tell an unfamiliar Agent:

- when the project workflow applies;
- required entry state;
- canonical stages/branches;
- purpose/input/output/gate for each top-level stage;
- which sub-Skill owns detailed procedure;
- when execution must stop.

Detailed schemas, algorithms, scientific rules, commands, and repair logic remain in
sub-Skills/references.

## New-project onboarding

For a new or structurally unclear water research repository:

```text
User identifies project
→ ChatGPT reads agent-collaboration
→ ChatGPT reads project-architecture.md
→ ChatGPT inspects actual repository/responsibilities
→ User + ChatGPT settle project boundaries
→ ChatGPT instantiates root AGENTS.md from project-agents-template.md
→ if an Agent-operable workflow exists, choose <agent-name>/ and instantiate its
  SKILL.md from project-skill-template.md
→ add only conditional directories with real responsibilities
→ Codex is delegated only when actual local execution/discovery/runtime verification
  is required
```

## Project-owned collaboration assets

Project-specific collaboration artifacts remain in that project:

```text
reports/concept/   durable User + ChatGPT project conclusions
reports/chatgpt/   implementation-ready ChatGPT task specifications
reports/codex/     Codex execution/verification evidence
```

Create these directories when their first owned artifact exists; empty scaffolding is
not required.

`agent-collaboration` owns only shared collaboration rules, project/Skill templates,
and global policy.

## ChatGPT entry flow

```text
project repository
→ project AGENTS.md
→ canonical agent-collaboration/SKILL.md
→ only needed collaboration references
→ project concept index when needed
→ declared project workflow SKILL.md when needed
→ owning sub-Skill/reference
→ User + ChatGPT design/decision
→ direct ChatGPT action when fully supported
→ Codex formal task only for genuinely local/unavailable capabilities
```

## Codex entry flow

```text
~/.codex/AGENTS.md
→ /Users/wenv/Documents/skills/agent-collaboration/SKILL.md
→ project AGENTS.md
→ project concept index when relevant
→ declared project workflow SKILL.md / owning sub-Skill
→ committed ChatGPT task
```

## Authority split

```text
agent-collaboration
= global User ↔ ChatGPT ↔ Codex collaboration rules + reusable templates

project AGENTS.md
= project constitution and repository-level routing

project <agent-name>/SKILL.md (when present)
= Agent-facing composite/project workflow router

project downstream Skills
= bounded capability procedures

project reports/concept/
= durable User + ChatGPT project conclusions

project reports/chatgpt/
= implementation-ready Codex task specifications

project reports/codex/
= Codex execution and verification evidence
```

## Design versus execution

User + ChatGPT own architecture, scientific/product semantics, workflow boundaries,
trust-state meanings, and acceptance criteria. Codex executes approved committed
specifications. It may report contradictions, missing prerequisites, or genuinely
unresolved human decisions, but it must not silently redesign approved behavior.
