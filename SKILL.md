---
name: agent-collaboration
description: >
  Coordinate User, ChatGPT, and Codex for repository work. Use when work needs
  project authority/routing, Codex delegation, local execution, verification,
  multi-conversation resume, project governance, Design maintenance, or maintained Skill development.
---

# Agent Collaboration

Canonical source: `cigit-zgy/agent-collaboration`.

Use this file as a thin router. Read only the owner needed for the active concern.

## Operating model

```text
User    = goals + scientific/product/design decisions + explicit checkpoints + final override
ChatGPT = design partner + connected author/executor + Codex-task author + acceptance reviewer
Codex   = local implementation/execution/verification/repair; never self-accepts
```

Explicit User instructions take precedence over generic collaboration guidance.

## Default behavior

For routine, reversible work inside an authorized scope:

```text
infer reasonable intent
→ inspect the relevant owner/state
→ act
→ verify proportionately
→ repair issues caused by the change
→ continue until the requested outcome is complete
```

Stop for User input only when missing information could materially change scientific/product meaning, an irreversible/destructive action, security/credentials/permission, public/release/external side effects, or an explicit User checkpoint.

## Direct routing

| Active concern | Primary owner |
|---|---|
| roles / precedence / decision boundaries | `references/collaboration/protocol.md` |
| DIRECT / LOCAL-QUICK / FORMAL / local state | `references/collaboration/execution.md` |
| FORMAL task / report / acceptance / integration | `references/collaboration/formal.md` |
| implementation quality / dependency reuse | `references/collaboration/implementation.md` |
| verification proportionality | `references/collaboration/verification.md` |
| project architecture | `references/project/architecture.md` |
| project governance / artifact admission / drift | `references/project/governance.md` |
| normal resume / `CURRENT.md` | `references/project/current.md` |
| Design reconciliation / report-to-Design sync | `references/project/reconciliation.md` |
| existing-project migration | `references/project/migration.md` |
| reports / layout | `references/project/reports.md` |
| explicit User-requested Concept | `references/project/concept.md` |
| current living Design | `references/project/design.md` |
| prior-art / reuse gate | `references/project/prior-art.md` |
| conversation handoff | `references/project/handoff.md` |
| first-party Skill development | `references/skill/development.md` |
| Skill writing / progressive disclosure | `references/skill/writing.md` |

Use one primary owner. Add a second only when the concern genuinely spans both responsibilities.

## Project state model

```text
current accepted Design      → reports/design/ or declared self-hosting operational owner
ChatGPT historical work      → reports/chatgpt/
Codex historical execution   → reports/codex/
explicit Concept history     → reports/concept/
conversation boundary        → reports/handoff/
current work edge            → CURRENT.md
```

Historical report families are append-only. Current Design is replace-in-place.

Project-specific canonical artifacts, scientific objects, source packages, and purity rules belong to the project that owns them, not to this generic collaboration Skill.

## Design synchronization

Do not wait for a scheduled summary when an accepted Design consequence is already known: update the owning current Design topic in the same work unit.

Use `project/reconciliation.md` as the backstop for accumulated/missed report deltas.

## Codex delegation

Every repository task delegated to Codex is committed under `reports/chatgpt/`; chat carries only the immutable locator.

Every Codex repository task leaves an append-only `reports/codex/` record:

```text
LOCAL-QUICK → concise Codex record
FORMAL      → richer Codex report → ChatGPT acceptance
```

Task prompts specify intended outcome, authority/boundaries, completion criteria, required evidence, and true decision boundary. Avoid command-by-command itineraries unless the commands themselves are the contract.

## Verification

Use the smallest evidence set that establishes the requested claim. Run broader or repeated checks only when risk, failures, new changes, or unresolved concerns justify them.

## Conversation resume

Normal resume:

```text
AGENTS.md → CURRENT.md → one directly relevant current owner
```

When the User explicitly switches conversation, create one compact handoff, point CURRENT to it, and return only the compact resume prompt owned by `project/current.md`.

## Cold paths

Do not preload Concept history, old tasks/reports/handoffs, archive, templates, or the full Design/reference tree. Load them only when the active concern requires them.
