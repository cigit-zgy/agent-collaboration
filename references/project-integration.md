# Project integration contract

This reference defines how an individual project repository connects to the global
`agent-collaboration` protocol without moving project-specific work into the
`agent-collaboration` repository.

## Project entry point

Each project repository uses its root `AGENTS.md` as the project-level entry point.
It is the project constitution and router, not a copy of the global collaboration
protocol.

A project `AGENTS.md` should identify:

- the project's purpose and scope;
- project-specific scientific, product, architectural, and safety authorities;
- the canonical collaboration repository;
- the Codex local collaboration entry;
- the project root `SKILL.md` or other project workflow router;
- the project concept index;
- the project report locations;
- any project-specific precedence or trust-state rules.

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

Do not copy the detailed global protocol, verification levels, report templates, or
Git synchronization procedure into each project `AGENTS.md`.

## Standard project `AGENTS.md` template

The canonical reusable template is:

`references/project-agents-template.md`

Use it when:

- onboarding a new project into this collaboration model;
- creating a root `AGENTS.md` for a repository that lacks one;
- normalizing an existing project entry that has accumulated stale routing or global
  rules that belong in `agent-collaboration`.

The template is a design scaffold, not a generated file that should be copied
unchanged. User + ChatGPT inspect the actual repository, decide the project-specific
purpose, authority, ownership, trust, runtime, workflow, and human checkpoints, then
instantiate only the applicable sections.

Onboarding follows:

```text
User identifies new project
→ ChatGPT reads agent-collaboration
→ ChatGPT reads project-agents-template.md
→ ChatGPT inspects the target repository
→ User + ChatGPT resolve project-specific design
→ ChatGPT writes/commits project AGENTS.md when connected tools are sufficient
→ Codex is delegated only if local discovery/state verification is genuinely needed
```

Do not delegate constitution design to Codex. Codex may verify that the committed
project entry is discovered correctly on the local machine, but the content of the
project constitution is a User + ChatGPT design decision.

## Project-owned assets

Every project's collaboration assets remain in that project's own repository:

```text
<project>/
├── AGENTS.md
├── SKILL.md
└── reports/
    ├── chatgpt/
    ├── codex/
    └── concept/
```

`agent-collaboration` owns only the shared collaboration rules and templates. It must
not become a central storage repository for project tasks, Codex reports, or project
concept decisions.

## ChatGPT entry flow

For a new ChatGPT conversation, the User normally supplies the project repository
and explicitly asks to use `agent-collaboration`.

ChatGPT then follows this order:

```text
project repository
→ project AGENTS.md
→ canonical agent-collaboration/SKILL.md
→ only needed collaboration references
→ project reports/concept/README.md
→ only relevant concept topics
→ project SKILL.md / relevant sub-Skill
→ User + ChatGPT design and decision
→ direct ChatGPT action when fully supported
→ Codex formal task only for genuinely local/unavailable capabilities
```

If the target repository has no suitable root `AGENTS.md`, ChatGPT first follows the
standard project template workflow above before proceeding to project implementation.

The project `AGENTS.md` is therefore the bridge from the project repository to the
shared collaboration authority.

## Codex entry flow

Codex normally enters from the machine-wide policy:

```text
~/.codex/AGENTS.md
→ /Users/wenv/Documents/skills/agent-collaboration/SKILL.md
→ project AGENTS.md
→ project reports/concept/README.md when relevant
→ project SKILL.md / relevant sub-Skill
→ committed ChatGPT task
```

Project `AGENTS.md` may add more specific project rules, but it must not silently
replace the global collaboration roles or report ownership model.

## Authority split

Use this interpretation consistently:

```text
agent-collaboration
= how User, ChatGPT, and Codex collaborate

project AGENTS.md
= project constitution and project-level routing

project SKILL.md
= project workflow/router

project reports/concept/
= durable User + ChatGPT project conclusions

project reports/chatgpt/
= implementation-ready Codex task specifications

project reports/codex/
= Codex execution and verification evidence
```

## Design versus execution

User + ChatGPT own design. ChatGPT should resolve and record architecture, behavior,
scientific/product semantics, scope, constraints, and acceptance criteria before a
Codex handoff whenever those decisions can reasonably be made remotely.

Codex executes the approved specification. Codex may report a contradiction,
missing local prerequisite, infeasible instruction, or genuinely unresolved human
decision, but it must not silently redesign an approved solution. Incidental coding
mechanics are allowed only when they do not change approved behavior, architecture,
scientific/product semantics, or task boundaries.
