# Project AGENTS.md template

Read `../../collaboration/agents.md` first. Keep project `AGENTS.md` concise and scope-local: declare project authority, ownership, routing, tooling, and genuine trust boundaries; route global collaboration policy to its owning references instead of copying it.

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
→ tests                                    conformance verification
→ <registered source/evidence path>         model/domain-specific scientific facts, when applicable
```

`reports/handoff/`, when present, is conversation context only and never overrides current design/task/source authority.

## Ownership

```text
<path>  <responsibility>
```

List only boundaries that materially affect Agent behavior.

## Workflow

Routine:

```text
AGENTS.md → <workflow>/SKILL.md → owning reference/script
```

Design / conformance:

```text
AGENTS.md → reports/concept/README.md → governing concept → projection → implementation/tests
```

For a new project/core subsystem or major algorithm/architecture redesign, run the current `agent-collaboration` prior-art gate before concept freeze.

When `reports/handoff/README.md` exists, context recovery is:

```text
AGENTS.md → reports/handoff/README.md → current handoff only → re-resolve current authority/state
```

## Runtime and tooling

<Project runtime/tooling authority and only the stable common commands an Agent actually needs.>

Project-specific shared coding-Skill additions: `<NONE OR PROJECT-OWNED IMMUTABLE COORDINATES>`.
Global implementation, verification, Git, shared-Skill, prior-art, and handoff policy comes from the current/pinned `cigit-zgy/agent-collaboration` authority.

## Human / trust checkpoints

<Only genuine project-specific scientific/product/trust decisions.>

## Hard invariants

- <Short project-wide boundary.>
- <Short project-wide boundary.>
````

Do not expand this template with task plans, implementation history, global collaboration rules, detailed verification policy, or copied prior-art/handoff manuals. Point to the owning artifact instead.
