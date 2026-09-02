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

User + ChatGPT own Skill design. Codex executes approved local work.

## Source / discovery / distribution

```text
maintained source
/Users/wenv/Documents/skills/<skill-name>/

Codex user discovery
$HOME/.agents/skills/<skill-name>
→ normally symlink → maintained source

portable runtime
SKILL.md + only required runtime resources
```

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

## Workflow

Use `SKILL.md` for capability operation and `references/skill/*` from agent-collaboration for repository/package policy when maintaining the Skill itself.

## Runtime and verification

<No independent runtime | runtime authority + stable verification route.>

## Hard invariants

<Short list of real source/discovery/ownership boundaries.>
````

Embedded sub-Skills normally inherit the nearest project `AGENTS.md`; a separate local file is justified only by real subtree-specific maintenance rules.
