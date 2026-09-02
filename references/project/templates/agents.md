# Project AGENTS.md template

Read `../../collaboration/agents.md` first. This template specializes that writing standard for a maintained scientific/software project.

````markdown
# <PROJECT_NAME> project context

## Identity

<What this project produces and the repository scope.>

## Authority

User + ChatGPT own project design. Codex executes approved local work.

```text
reports/concept/                 canonical accepted design, when declared
<workflow>/SKILL.md + references operational projection
scripts/code/schemas             implementation
tests                            conformance verification
registered source/evidence       model-specific scientific fact authority
```

## Repository ownership

```text
<path>  <responsibility>
```

List only ownership boundaries that affect Agent behavior.

## Workflow

Project workflow Skill: `<PROJECT-DECLARED-SKILL-PATH>`

Routine:

```text
AGENTS.md
→ workflow SKILL.md
→ owning sub-Skill
→ required reference/script
```

Design/redesign/conformance:

```text
AGENTS.md
→ reports/concept/README.md
→ governing concept
→ affected Skill/reference
→ implementation/tests
```

## Runtime and verification

<Runtime/tooling authority and stable common commands, if any.>

## Human / trust checkpoints

<Only genuine project-specific decisions or trust transitions.>

## Hard invariants

<Short project-wide hard boundaries.>
````

A project `AGENTS.md` routes to `agent-collaboration` for global collaboration/Git/verification mechanics rather than copying those manuals.
