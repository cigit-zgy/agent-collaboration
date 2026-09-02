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

User + ChatGPT maintain collaboration design. ChatGPT independently reviews execution evidence; the User retains final decision/override authority. Codex executes approved local work.

## Repository ownership

```text
references/collaboration/   three-party protocol, verification, AGENTS writing, task/report templates
references/project/         project integration, concept policy, project templates
references/skill/           Skill repository/package/writing policy and Skill-repository template
reports/concept/             collaboration decision history/rationale
reports/chatgpt/             committed formal local-execution specifications
reports/codex/               formal Codex execution evidence
```

Each concern has one current operational owner under `references/`.

## Routing

Read `SKILL.md` first for collaboration work, then load only the owning reference for the active topic.

```text
collaboration behavior → references/collaboration/
project integration     → references/project/
Skill design/maintenance→ references/skill/
```

For authoring or reviewing repository/project `AGENTS.md`, use `references/collaboration/agents.md` before the relevant project/Skill specialization.

Maintained-source location, Codex discovery exposure, and external distribution are owned by `references/skill/repository.md`; this `AGENTS.md` does not duplicate installation-specific paths.

## Runtime and verification

This repository owns no independent runtime by default. Documentation-only changes use direct structural/link review. Executable verification follows `references/collaboration/verification.md` only when executable behavior is actually introduced or changed.

Codex execution mode selection—routine local execution versus formal delegated task—is owned by `references/collaboration/protocol.md`.

## Hard invariants

- Current operational policy has one owner under `references/`.
- Formal task/report artifacts remain stable after issue.
- Project-specific scientific/design truth remains in the owning project.
- Repository restructuring preserves the meaning and active routing of current policy.
- Installation-specific source/discovery paths have one owner in `references/skill/repository.md`.
