# Project AGENTS.md template

Read `../../collaboration/agents.md` first. Keep project `AGENTS.md` concise and scope-local: declare project authority, ownership, workflow entry, tooling, and genuine trust boundaries. Route global collaboration behavior through the current/pinned `agent-collaboration/SKILL.md`; do not copy collaboration manuals.

````markdown
# <PROJECT_NAME> context

## Identity

<One or two sentences: what this repository produces and owns.>

## Authority

```text
explicit User instruction
→ reports/concept/                         accepted project design, when declared
→ <workflow>/SKILL.md + references         operational workflow
→ <implementation paths>                   implementation
→ tests                                    conformance/design evidence
→ <registered source/evidence path>         model/domain-specific scientific facts, when applicable
```

`reports/handoff/`, when present, is conversation context only and never overrides current design/task/source authority.

Global collaboration authority:
`cigit-zgy/agent-collaboration@<COLLABORATION_REVISION>`

Runtime collaboration entry:
`SKILL.md`

Do not preload the collaboration reference tree. Resolve the active intent through that Skill and read only the selected owner(s).

## Ownership

```text
<path>  <responsibility>
```

List only boundaries that materially affect Agent behavior.

`tmp/` is the project-local Agent ephemeral boundary; detailed local execution/Git/worktree semantics come from the collaboration `execution.md` owner selected through `SKILL.md`.

## Workflow

Routine:

```text
AGENTS.md
→ <workflow>/SKILL.md
→ owning project reference/script
```

Design / conformance:

```text
AGENTS.md
→ reports/concept/README.md
→ governing concept
→ projection
→ implementation/tests
```

For a new project/core subsystem or major algorithm/architecture/tool choice, use the current collaboration prior-art route before concept freeze.

For an evolving external CLI/API/schema/parser/simulator concern, use the collaboration external-tool route directly; do not copy adapter policy here.

When `reports/handoff/README.md` exists, context recovery is:

```text
AGENTS.md
→ reports/handoff/README.md
→ current handoff only
→ re-resolve current authority/state
```

## Runtime and tooling

<Project runtime/tooling authority and only stable common commands an Agent actually needs.>

Project-specific shared coding-Skill additions:
`<NONE OR PROJECT-OWNED IMMUTABLE COORDINATES>`

Global implementation, verification, Actions, Git/local execution, FORMAL delegation, prior-art, external-tool, and handoff policy is discovered through the current/pinned collaboration `SKILL.md` direct routing table.

## Human / trust checkpoints

<Only genuine project-specific scientific/product/trust decisions.>

## Hard invariants

- <Short project-wide boundary.>
- <Short project-wide boundary.>
````

Do not expand this template with task plans, implementation history, global collaboration rules, detailed verification policy, or copied prior-art/handoff manuals. Point to the owning project artifact or collaboration route instead.
