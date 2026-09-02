# Project `AGENTS.md` template

Use this template when onboarding a repository into the `agent-collaboration`
workflow. Root `AGENTS.md` is the project-level entry point and constitution. Keep
it concise, stable, and project-specific; do not copy the detailed global
collaboration protocol into it.

Replace placeholders, remove sections that are genuinely not applicable, and keep
only rules that are durable for the project.

```markdown
# <PROJECT_NAME> project context

## Project identity

<ONE-TO-THREE SENTENCES: what this project is, what it produces, and its primary
purpose.>

## Scope and precedence

This repository follows the global User ↔ ChatGPT ↔ Codex collaboration protocol.

Canonical collaboration repository:
`cigit-zgy/agent-collaboration`

Codex local collaboration entry:
`/Users/wenv/Documents/skills/agent-collaboration/SKILL.md`

Project-specific scientific, product, architectural, safety, and trust-state rules
in this repository are authoritative for this project. Do not duplicate the global
collaboration protocol here.

User + ChatGPT own design decisions. Codex executes approved implementation-ready
specifications and must not silently redesign them.

## Project boundaries

- <CORE IN-SCOPE RESPONSIBILITY>
- <IMPORTANT OUT-OF-SCOPE RESPONSIBILITY>
- <BOUNDARY BETWEEN PRODUCTION CODE AND PROJECT/USER ARTIFACTS, IF RELEVANT>
- <OTHER DURABLE PROJECT BOUNDARY>

## Authority and trust

<STATE THE PROJECT'S SOURCE-OF-TRUTH OR AUTHORITY ORDER.>

Example forms:

```text
source evidence
→ derived representation
→ validated state
→ approved/released state
```

or, for a non-scientific project:

```text
project contract
→ implementation
→ verification evidence
→ accepted release
```

Define any project-specific trust states here. Do not invent trust states merely
because the template provides this section.

## Repository ownership

```text
<path>/    <durable responsibility>
<path>/    <durable responsibility>
reports/   collaboration tasks, execution evidence, and durable project concepts
```

State read-only or immutable directories explicitly when they exist. Do not list
every directory; list only ownership boundaries that affect Agent behavior.

## Project knowledge and reports

Project collaboration assets remain in this repository:

```text
reports/
├── chatgpt/    implementation-ready Codex task specifications
├── codex/      Codex execution and verification evidence
└── concept/    durable User + ChatGPT project conclusions
```

Read `reports/concept/README.md` first when durable design context is needed, then
read only the concept topics relevant to the current task.

Report metadata, archival rules, and task/report lifecycle follow the canonical
`agent-collaboration` policy.

## Workflow routing

Project workflow router:
`<PROJECT_SKILL_OR_ROUTER_PATH>`

Read the root router before selecting a downstream Skill or workflow. Do not infer a
downstream stage that the project does not define.

<OPTIONAL: short list of stable top-level workflow stages, without duplicating the
sub-Skill manuals.>

## Runtime and environment

<STATE THE PROJECT'S RUNTIME/ENVIRONMENT AUTHORITY, OR "No project runtime".>

Examples:

```text
Environment: <ENVIRONMENT_NAME>
Dependency/tooling authority: <pyproject.toml | package.json | other contract>
```

Environment creation, dependency mutation, broad verification, Git synchronization,
and security-tool selection follow the global collaboration policy unless this
project explicitly requires a stricter rule.

## Human checkpoints

<LIST ONLY DECISIONS THAT GENUINELY REQUIRE HUMAN AUTHORITY.>

If none are project-specific, write:

`No additional project-specific human checkpoints beyond the global collaboration
protocol.`

## Non-negotiable project invariants

- <INVARIANT 1>
- <INVARIANT 2>
- <INVARIANT 3>

Keep this list short. Detailed implementation behavior belongs in project Skills,
contracts, or concept files rather than in `AGENTS.md`.
```

## Onboarding procedure

For a new project repository:

```text
User identifies the project
→ ChatGPT reads agent-collaboration
→ ChatGPT reads this template
→ ChatGPT inspects the target repository
→ User + ChatGPT resolve project-specific decisions
→ ChatGPT writes the project's root AGENTS.md when its connected tools can do so
→ project AGENTS.md becomes the project entry point
→ local Codex verification is delegated only when actual local discovery/state must be tested
```

Do not delegate creation of the project constitution to Codex merely because Codex
can edit the local file. The constitution is a User + ChatGPT design artifact. Codex
may verify local discovery after the design is committed.

## Quality criteria

A good project `AGENTS.md` should answer, quickly:

1. What is this project?
2. Which project rules are authoritative?
3. How does the project connect to `agent-collaboration`?
4. Where are durable concepts and collaboration reports?
5. What project Skill/router should be read next?
6. What are the main ownership/trust boundaries?
7. Which runtime/environment contract applies?
8. Which decisions require a human?

If the file starts explaining detailed implementation steps, test commands,
sub-Skill internals, or global Git/verification procedure, move that detail to the
owning Skill/reference instead.
