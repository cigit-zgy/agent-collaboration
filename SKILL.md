---
name: agent-collaboration
description: Use as the shared collaboration hub for User, ChatGPT, and Codex when repository work requires planning, direct remote action, local execution handoff, verification, independent audit, acceptance, project onboarding, or durable project concept assets.
---

# Agent Collaboration

This Skill is the shared operating hub for the three-party workflow:

```text
User ↔ ChatGPT ↔ Codex
```

The User is the human authority. ChatGPT plans, resolves what can be made explicit,
performs work it can safely complete through its available connected tools, authors
formal Codex tasks only when local execution is genuinely required, and independently
accepts or rejects Codex results. Codex executes committed local tasks and returns
verifiable implementation evidence.

## Entry points

- **Codex:** machine-wide `~/.codex/AGENTS.md` routes formal ChatGPT ↔ Codex
  repository work to this Skill automatically.
- **ChatGPT:** a new conversation does not assume this local Skill automatically.
  The User should explicitly ask ChatGPT to use `agent-collaboration` and provide or
  identify the target project repository. ChatGPT reads the project's root
  `AGENTS.md`, follows its canonical collaboration reference to this Skill, and then
  reads only the collaboration references needed for the active role.
- **Project repository:** root `AGENTS.md` is the project-level entry point and
  constitution. The project root `SKILL.md` is the Agent-facing workflow/router.
  Together they connect global collaboration, durable project concepts, and
  downstream stage Skills without copying detailed global rules.
- **New project:** when a repository does not yet have suitable project entry assets,
  User + ChatGPT design `AGENTS.md` from
  [project-agents-template.md](references/project-agents-template.md), then design the
  root workflow Skill from
  [project-skill-template.md](references/project-skill-template.md). ChatGPT writes
  and commits those design assets directly when its connected tools can do so;
  Codex is used only for genuinely local verification or other unavailable
  capabilities.
- **User:** defines goals, approves genuine human decisions, and may override the
  workflow explicitly.

Project-specific tasks, Codex reports, and concept decisions always remain in the
project repository that owns them. This repository owns the collaboration protocol
and reusable templates, not other projects' work records.

## Delegation rule

Do not delegate work to Codex merely because Codex can do it. Before issuing a Codex
task, ChatGPT must first determine whether it can safely and completely perform the
work itself with available connected tools. If yes, ChatGPT performs and verifies it
directly. Codex receives only work that genuinely requires local-machine execution,
local repository state, local CLI/runtime access, environments, secrets/credentials,
large local builds, or another capability unavailable to ChatGPT.

When Codex is required, ChatGPT removes avoidable design ambiguity first. User +
ChatGPT own design; Codex executes the approved implementation-ready specification.
The formal task should contain the concrete files, decisions, constraints, commands
when useful, acceptance criteria, verification level, report path, and fixed stdout
needed for Codex to execute rather than redesign the task.

One formal Codex task is active at a time. Evidence, not a self-reported PASS,
determines completion.

## References

- All roles: read [protocol.md](references/protocol.md) for responsibilities,
  entrypoints, delegation boundaries, repository synchronization, and the
  collaboration loop.
- Connecting an individual project repository to this global protocol: read
  [project-integration.md](references/project-integration.md).
- Creating or normalizing a project's root `AGENTS.md`: use
  [project-agents-template.md](references/project-agents-template.md).
- Creating or normalizing a project's root workflow `SKILL.md`: use
  [project-skill-template.md](references/project-skill-template.md).
- ChatGPT authoring a Codex task: use
  [chatgpt-task-template.md](references/chatgpt-task-template.md) and select a
  level from [verification-levels.md](references/verification-levels.md).
- Choosing security/static/dependency verification tools: read
  [verification-tools.md](references/verification-tools.md).
- Creating, reusing, or rebuilding a Skill/project environment: read
  [skill-environment-policy.md](references/skill-environment-policy.md).
- ChatGPT handing off a committed task: use
  [codex-launch-template.md](references/codex-launch-template.md).
- Codex reporting work, or ChatGPT auditing it: use
  [codex-report-template.md](references/codex-report-template.md).
- Creating, archiving, or maintaining `reports/chatgpt/`, `reports/codex/`, or
  durable `reports/concept/` assets: read
  [report-concept-policy.md](references/report-concept-policy.md).
- Maintaining a Skill repository: read
  [skill-repository-policy.md](references/skill-repository-policy.md).
