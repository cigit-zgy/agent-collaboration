---
id: 02
title: Three-party Collaboration Hub
status: active
created: 2026-09-02
updated: 2026-09-02
authority: global
scope: shared User-ChatGPT-Codex authority, entrypoints, delegation boundary, and task freezing
supersedes: null
related_tasks: []
---

# Three-party Collaboration Hub

## 2026-09-02

### Decision

`agent-collaboration` is the shared operating authority for the three-party workflow:

```text
User ↔ ChatGPT ↔ Codex
```

The roles enter this authority differently:

- Codex is routed to the Skill automatically by machine-wide `~/.codex/AGENTS.md` for formal ChatGPT ↔ Codex repository work.
- ChatGPT must be explicitly told by the User in a new conversation to use `agent-collaboration`, or be given the repository. ChatGPT then reads the current Skill and only the references relevant to its role.
- The User remains the final human authority for goals, scientific/product decisions, and genuine human-only ambiguity.

ChatGPT is not merely a task writer. Before delegation it must decide whether Codex is actually necessary. If ChatGPT can safely and completely perform and verify the work using its available connected tools, ChatGPT performs it directly. Codex is reserved for work that genuinely requires local-machine state or another unavailable capability, including local filesystem/worktree state, CLI/runtime execution, environments, local tests/builds/rendering, credentials/services, or other machine-local operations.

When Codex is required, ChatGPT must freeze all reasonably determinable decisions before handoff. The committed task should leave Codex execution work rather than avoidable design work: scope, authoritative sources, affected files/areas, approved behavior, non-goals, engineering constraints, verification level, acceptance criteria, Git requirements, report path, fixed stdout, and exact commands/replacement text when useful.

A formal Codex task therefore includes an explicit `Why Codex is required` statement. If no concrete local or unavailable capability can be named, the task should not be delegated.

### Rationale

A single shared authority prevents ChatGPT prompts, Codex global rules, and project-specific notes from drifting into incompatible collaboration models. Minimizing delegation reduces unnecessary handoffs and lets ChatGPT use its stronger planning/context capabilities to resolve ambiguity before local execution. Codex remains valuable where the work genuinely depends on the User's machine or runtime.

### Impact

- `SKILL.md`
- `references/protocol.md`
- `references/chatgpt-task-template.md`
- `~/.codex/AGENTS.md` as the Codex entry route
- future User instructions that explicitly activate this Skill for ChatGPT
- project `AGENTS.md` files, which should route to this Skill rather than duplicate the collaboration protocol

### Related tasks

None. This decision was applied directly by ChatGPT through connected repository tooling because it did not require local-machine execution.
