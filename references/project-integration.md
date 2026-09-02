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

Do not delegate constitution design to Codex. Codex may verify that the committed
project entry is discovered correctly on the local machine, but the content of the
project constitution is a User + ChatGPT design decision.

## Standard project root `SKILL.md` template

The canonical reusable workflow template is:

`references/project-skill-template.md`

Use it after the project constitution is known. The root project Skill is the
Agent-facing workflow/router: it tells an unfamiliar Agent when the project workflow
applies, the required entry state, the canonical top-level stages, each stage's
purpose/input/output/gate, which downstream Skill owns the detailed procedure, and
when the Agent must stop rather than infer.

The root project Skill must not become a second `AGENTS.md` or a monolithic manual.
Use progressive disclosure:

```text
project AGENTS.md
→ project concept index when needed
→ project root SKILL.md
→ owning downstream Skill
→ only required references/scripts
```

For each real top-level stage, prefer five routing facts:

```text
purpose
required input
stable output
next-stage gate
owning Skill
```

Detailed schemas, algorithms, scientific rules, command sequences, and repair logic
belong in downstream Skills/references rather than in the root router.

User + ChatGPT own workflow design. Codex may verify the committed Skill against
actual local runtime/discovery behavior, but it must not silently redesign approved
stage semantics or trust boundaries.

## New-project onboarding

For a repository that does not yet have suitable project entry assets:

```text
User identifies new project
→ ChatGPT reads agent-collaboration
→ ChatGPT reads project-agents-template.md
→ ChatGPT inspects the target repository
→ User + ChatGPT resolve project constitution decisions
→ ChatGPT writes/commits project AGENTS.md when connected tools are sufficient
→ ChatGPT reads project-skill-template.md
→ User + ChatGPT resolve canonical workflow/stage boundaries
→ ChatGPT writes/commits project root SKILL.md when connected tools are sufficient
→ Codex is delegated only if local discovery/runtime/state verification is genuinely needed
```

Project-entry design is not a default Codex task.

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
→ project root SKILL.md / relevant sub-Skill
→ User + ChatGPT design and decision
→ direct ChatGPT action when fully supported
→ Codex formal task only for genuinely local/unavailable capabilities
```

If the target repository has no suitable root `AGENTS.md` or project root Skill,
ChatGPT first follows the standard onboarding workflow above before proceeding to
project implementation.

The project `AGENTS.md` is the bridge from the project repository to the shared
collaboration authority; the project root `SKILL.md` is the bridge from project
governance into executable workflow routing.

## Codex entry flow

Codex normally enters from the machine-wide policy:

```text
~/.codex/AGENTS.md
→ /Users/wenv/Documents/skills/agent-collaboration/SKILL.md
→ project AGENTS.md
→ project reports/concept/README.md when relevant
→ project root SKILL.md / relevant sub-Skill
→ committed ChatGPT task
```

Project `AGENTS.md` may add more specific project rules, but it must not silently
replace the global collaboration roles or report ownership model.

## Authority split

Use this interpretation consistently:

```text
agent-collaboration
= how User, ChatGPT, and Codex collaborate + reusable project-entry templates

project AGENTS.md
= project constitution and project-level routing

project root SKILL.md
= Agent-facing project workflow/router

project downstream Skills
= detailed stage-specific procedures and references

project reports/concept/
= durable User + ChatGPT project conclusions

project reports/chatgpt/
= implementation-ready Codex task specifications

project reports/codex/
= Codex execution and verification evidence
```

## Design versus execution

User + ChatGPT own design. ChatGPT should resolve and record architecture, behavior,
scientific/product semantics, workflow stages, scope, constraints, and acceptance
criteria before a Codex handoff whenever those decisions can reasonably be made
remotely.

Codex executes the approved specification. Codex may report a contradiction,
missing local prerequisite, infeasible instruction, or genuinely unresolved human
decision, but it must not silently redesign an approved solution. Incidental coding
mechanics are allowed only when they do not change approved behavior, architecture,
workflow semantics, scientific/product semantics, or task boundaries.
