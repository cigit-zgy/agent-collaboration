# Maintained Skill-repository AGENTS.md template

Read `../../collaboration/agents.md` first. Use this specialization for a standalone maintained first-party Skill source repository.

````markdown
# <SKILL_NAME> repository context

## Identity

This repository is the maintained first-party source for the `<SKILL_NAME>` Skill.

<One concise capability/repository description.>

## Authority

```text
AGENTS.md    repository maintenance/routing
SKILL.md     Agent-facing capability/workflow entry
references/  Skill-specific operational contracts
reports/     collaboration/history assets when this repository owns them
```

User + ChatGPT maintain Skill design. ChatGPT performs connected DIRECT work and acceptance review; the User retains final decision/override authority and designated human checkpoints. Codex executes approved LOCAL implementation/execution. Zero-human-coding is permitted.

## Repository ownership

```text
SKILL.md        <responsibility>
references/     <if present>
scripts/        <if present>
assets/         <if present>
tests/          <if present>
pyproject.toml  <if present>
README.md       <if present>
```

List only real paths.

## Source / discovery / distribution

Use `agent-collaboration/references/skill/repository.md` as the owner of maintained-source location, Codex discovery exposure, and external distribution policy. State repository-local exceptions here only when this Skill genuinely differs from that policy.

## Workflow

Use `SKILL.md` for capability operation and `references/skill/*` from agent-collaboration for repository/package/writing policy when maintaining the Skill itself. AI-assisted implementation follows `agent-collaboration/references/collaboration/implementation.md`.

## Runtime and verification

<No independent runtime | runtime authority + mechanical style/verification route.>

## Hard invariants

<Short list of real source/discovery/ownership boundaries that are specific to this repository.>
````

Embedded sub-Skills normally inherit the nearest project `AGENTS.md`; a separate local file is justified only by real subtree-specific maintenance rules.
