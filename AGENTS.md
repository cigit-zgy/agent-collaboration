# agent-collaboration repository context

## Identity

This repository is the maintained first-party source for the `agent-collaboration` Skill.

## Authority

```text
AGENTS.md
= repository-maintenance constitution

SKILL.md
= sole runtime routing index

references/
= current operational owners

reports/concept/
= collaboration decision history/rationale

reports/chatgpt/
= durable ChatGPT-authored Codex task specifications

reports/codex/
= FORMAL Codex execution evidence only
```

User + ChatGPT maintain collaboration design. The User retains final decision/override authority and designated checkpoints. ChatGPT performs connected DIRECT authoring and acceptance review. Codex executes approved LOCAL work and does not self-accept.

## Owner map

```text
references/collaboration/protocol.md
= roles / authority / refresh / trust

references/collaboration/execution.md
= DIRECT/LOCAL-QUICK/FORMAL + Git/worktree/tmp/remote sync

references/collaboration/formal.md
= FORMAL report/acceptance/integration

references/collaboration/implementation.md
= implementation discipline

references/collaboration/verification.md
= verification/evidence placement

references/collaboration/actions.md
= GitHub Actions policy

references/project/architecture.md
= project ownership/integration

references/project/current.md
= CURRENT.md + normal multi-conversation resume

references/project/migration.md
= existing-project collaboration migration

references/project/reports.md
= reports/design + chronological report-family/archive layout

references/project/concept.md
= chronological design history/input

references/project/design.md
= current living design under reports/design/

references/project/prior-art.md
= external prior-art/reuse gate

references/project/handoff.md
= exceptional conversation-only delta

references/skill/development.md
= current design → Skill Markdown → implementation → tests
```

Read `SKILL.md` first and load only the owning reference.

## Hard invariants

- `SKILL.md` is the sole runtime routing index.
- Long-running projects use root `CURRENT.md` only for NOW-state/work edge.
- Normal conversation resume is `AGENTS.md → CURRENT.md → reports/design/README.md`, not project migration and normally not handoff.
- `reports/handoff/` is exceptional residual conversation-only delta only.
- `reports/design/` is the single current living-design authority when explicit design is used; it is not a chronological report family.
- `reports/concept/` is design history/input only and never overrides `reports/design/`.
- No project keeps root `design/` and `reports/design/` as parallel current authorities.
- Every Codex repository task is committed under `reports/chatgpt/` before delegation; chat contains only the locator.
- LOCAL-QUICK creates no `reports/codex/` report; FORMAL does.
- Every repository-changing Codex task fresh-fetches before mutation and after push, proving exact local/authorized-remote equality at both boundaries.
- Remote synchronization does not authorize destructive Git alignment.
- Historical reports/templates/archive are cold unless directly needed.
- Skill behavior changes follow `reports/design/ → SKILL.md/references → implementation → design-probing tests`.
- Project-specific scientific facts remain in their owning source/evidence chain.
