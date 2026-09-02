# agent-collaboration repository context

## Identity

This repository is the maintained first-party source for the `agent-collaboration` Skill. It defines the reusable User ↔ ChatGPT ↔ Codex collaboration contract used across maintained projects and Skills.

## Authority

```text
AGENTS.md
= repository-maintenance constitution

SKILL.md
= collaboration entry and routing

references/
= current operational contracts

reports/concept/
= this repository's decision history/rationale

reports/chatgpt/ + reports/codex/
= formal task specifications and execution evidence
```

User + ChatGPT own collaboration design. Codex executes approved local work and supplies verification evidence.

## Repository ownership

```text
references/collaboration/   three-party protocol, verification, AGENTS writing, task/report templates
references/project/         project architecture, concept policy, project templates
references/skill/           Skill repository/package/writing policy and Skill-repository template
reports/concept/             collaboration decision history/rationale
reports/chatgpt/             committed local-execution specifications
reports/codex/               Codex execution evidence
```

Each concern has one current operational owner under `references/`.

## Routing

Read `SKILL.md` first for collaboration work, then load only the owning reference for the active topic.

```text
collaboration behavior → references/collaboration/
project integration     → references/project/
Skill design/maintenance→ references/skill/
```

For authoring or reviewing repository/project `AGENTS.md`, use `references/collaboration/agents.md` before the relevant project/Skill template.

## Source and discovery

Maintained source:

```text
/Users/wenv/Documents/skills/agent-collaboration/
```

Codex user-scoped discovery normally exposes that source through:

```text
$HOME/.agents/skills/agent-collaboration
```

Detailed ownership/discovery rules live in `references/skill/repository.md`.

## Runtime and verification

This repository owns no independent runtime by default. Documentation-only changes use direct structural/link review; executable verification follows `references/collaboration/verification.md` when a task actually introduces or changes executable behavior.

## Hard invariants

- Current operational policy has one owner under `references/`.
- Formal task/report artifacts remain stable after issue.
- Project-specific scientific/design truth remains in the owning project.
- Repository restructuring preserves the meaning and active routing of current policy.
