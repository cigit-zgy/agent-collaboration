# Project `AGENTS.md` template

Use this template when onboarding or normalizing a maintained project repository under
the `agent-collaboration` workflow. For water-domain research projects, first read
`project-architecture.md` and instantiate only the responsibilities the actual
repository owns.

Root `AGENTS.md` is the project-level entry point and constitution. Keep it concise,
stable, and project-specific; do not copy the detailed global collaboration protocol
into it.

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

Example scientific form:

```text
source evidence
→ derived representation
→ validated state
→ approved/released state
```

Define only real project-specific trust states.

## Repository ownership

List only directories that actually exist or are approved project responsibilities.
Use `project-architecture.md` as the responsibility map; do not scaffold every
optional path.

```text
<path>/    <durable responsibility>
<path>/    <durable responsibility>
reports/   collaboration tasks/evidence/concepts when such assets exist
```

State immutable/read-only boundaries explicitly when relevant.

## Project knowledge and reports

Project collaboration assets remain in this repository:

```text
reports/concept/   durable User + ChatGPT project conclusions
reports/chatgpt/   implementation-ready Codex task specifications
reports/codex/     Codex execution and verification evidence
```

Create report directories when the first owned artifact exists; empty scaffolding is
not required.

Read `reports/concept/README.md` first when durable design context is needed, then
only the concept topics relevant to the active task.

## Workflow routing

Canonical project workflow Skill:
`<PROJECT_WORKFLOW_SKILL_PATH OR "none">`

For a multi-Skill Agent project this will commonly be:

`<agent-name>/SKILL.md`

Do not create a duplicate repository-root `SKILL.md` when the real workflow router
already lives inside the Agent package. Read the declared workflow Skill before
selecting a downstream capability.

<OPTIONAL: short list of stable top-level workflow stages/capabilities.>

## Runtime and environment

<STATE THE PROJECT'S RUNTIME/ENVIRONMENT AUTHORITY, OR "No project runtime".>

Example:

```text
Environment: <ENVIRONMENT_NAME>
Dependency/tooling authority: <pyproject.toml | package.json | other contract>
```

Environment mutation, broad verification, Git synchronization, and security-tool
selection follow the global collaboration policy unless this project explicitly
requires a stricter rule.

## Human checkpoints

<LIST ONLY DECISIONS THAT GENUINELY REQUIRE HUMAN AUTHORITY.>

If none are project-specific:

`No additional project-specific human checkpoints beyond the global collaboration
protocol.`

## Non-negotiable project invariants

- <INVARIANT 1>
- <INVARIANT 2>
- <INVARIANT 3>

Keep this list short. Detailed implementation behavior belongs in Skills, contracts,
or concept files rather than `AGENTS.md`.
```

## Onboarding procedure

```text
User identifies project
→ ChatGPT reads agent-collaboration
→ ChatGPT reads project-architecture.md
→ ChatGPT inspects actual repository/responsibilities
→ User + ChatGPT resolve project-specific boundaries and authority
→ ChatGPT instantiates this AGENTS.md template
→ if an Agent-operable workflow exists, declare its canonical SKILL.md path
→ local Codex verification is delegated only when actual local discovery/state must
  be tested
```

Do not delegate creation of the project constitution to Codex merely because Codex
can edit the local file. The constitution is a User + ChatGPT design artifact.

## Quality criteria

A good project `AGENTS.md` should answer quickly:

1. What is this project?
2. Which project rules are authoritative?
3. How does it connect to `agent-collaboration`?
4. What responsibilities/directories does the repository actually own?
5. Where are durable concepts and collaboration reports?
6. What project workflow Skill, if any, should be read next?
7. What trust/runtime boundaries apply?
8. Which decisions require a human?

If the file starts explaining detailed implementation steps, experiment methods,
test commands, sub-Skill internals, or global Git/verification procedure, move that
detail to the owning Skill/reference/concept instead.
