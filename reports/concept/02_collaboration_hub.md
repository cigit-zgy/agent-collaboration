---
id: 02
title: Three-party Collaboration Hub
status: active
created: 2026-09-02
updated: 2026-09-02
authority: global
scope: shared User-ChatGPT-Codex authority, entrypoints, delegation boundary, design ownership, and task freezing
supersedes: null
related_tasks: []
---

# Three-party Collaboration Hub

## Current conclusion

`agent-collaboration` is the shared operating authority for the User ↔ ChatGPT ↔
Codex workflow. The User is the human authority. User + ChatGPT own design and
resolve every reasonably determinable architecture, scientific/product, behavioral,
scope, and acceptance decision before local execution. ChatGPT performs work it can
safely and completely execute with its connected tools and delegates only genuinely
local or otherwise unavailable capabilities. Codex executes the committed
implementation-ready specification, reports contradictions or design-affecting
ambiguity instead of silently redesigning, and returns verifiable evidence. ChatGPT
independently accepts or rejects the result.

Codex enters automatically through machine-wide `~/.codex/AGENTS.md`. ChatGPT is
explicitly directed by the User in a new conversation to use `agent-collaboration`
and the target project repository. Project-specific work records remain in the
owning project repository.

## Decision history

### 2026-09-02

#### Conclusion

The collaboration model is:

```text
User ↔ ChatGPT ↔ Codex
```

The roles enter this authority differently:

- Codex is routed to the Skill automatically by machine-wide `~/.codex/AGENTS.md`
  for formal ChatGPT ↔ Codex repository work.
- ChatGPT must be explicitly told by the User in a new conversation to use
  `agent-collaboration` and identify the target project repository.
- The User remains the final human authority for goals, scientific/product
  decisions, and genuine human-only ambiguity.

ChatGPT is not merely a task writer. Before delegation it decides whether Codex is
actually necessary. If ChatGPT can safely and completely perform and verify the work
using its available connected tools, ChatGPT performs it directly. Codex is reserved
for work that genuinely requires local-machine state or another unavailable
capability, including local filesystem/worktree state, CLI/runtime execution,
environments, local tests/builds/rendering, credentials/services, or other
machine-local operations.

User + ChatGPT own design. When Codex is required, ChatGPT freezes all reasonably
determinable decisions before handoff. The committed task should leave Codex
execution work rather than avoidable design work: scope, authoritative sources,
affected files/areas, approved behavior, non-goals, engineering constraints,
verification level, acceptance criteria, Git requirements, report path, fixed
stdout, and exact commands/replacement text when useful.

A formal Codex task therefore includes an explicit `Why Codex is required`
statement. If no concrete local or unavailable capability can be named, the task
should not be delegated.

Codex may report contradictions, infeasible instructions, missing local
prerequisites, or design-affecting ambiguity, but it must not silently choose a new
architecture, scientific/product meaning, behavior, or scope. Incidental coding
mechanics are permitted only when they preserve the approved design.

#### Rationale

A single shared authority prevents ChatGPT prompts, Codex global rules, and
project-specific notes from drifting into incompatible collaboration models.
Keeping design with User + ChatGPT exploits the interactive design stage before
execution. Minimizing delegation reduces unnecessary handoffs, while Codex remains
valuable where work genuinely depends on the User's machine or runtime.

#### Boundary

This concept governs collaboration roles and delegation. It does not define any
project's scientific or architectural content; those rules belong to that project's
own `AGENTS.md`, Skills, and concept assets.

#### Impact

- `SKILL.md`
- `references/protocol.md`
- `references/chatgpt-task-template.md`
- `~/.codex/AGENTS.md` as the Codex entry route
- project `AGENTS.md` files that route to this Skill
- future User instructions that explicitly activate this Skill for ChatGPT

#### Related tasks

None. The decision was applied directly by ChatGPT through connected repository
tooling because it did not require local-machine execution.
