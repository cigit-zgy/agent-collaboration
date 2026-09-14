---
name: agent-collaboration
description: >
  Coordinate User, ChatGPT, and Codex for repository work. Use when work needs
  project authority/routing, Codex delegation, local execution, verification,
  multi-conversation resume, project governance, or maintained Skill development.
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

For routine, reversible work inside an already-authorized scope:

```text
infer reasonable intent
→ inspect the relevant owner/state
→ act
→ verify proportionately
→ repair issues caused by the change
→ continue until the requested outcome is complete
```

Do not ask for confirmation merely because an intermediate implementation choice is underspecified.

Stop for User input only when missing information could materially change:

```text
scientific or product meaning
an irreversible/destructive action
security, credentials, or permission
public/release/external side effects
an explicit User checkpoint
```

## Direct routing

| Active concern | Primary owner |
|---|---|
| roles / precedence / decision boundaries | `references/collaboration/protocol.md` |
| DIRECT / LOCAL-QUICK / FORMAL / local state | `references/collaboration/execution.md` |
| FORMAL task / report / acceptance / integration | `references/collaboration/formal.md` |
| implementation quality | `references/collaboration/implementation.md` |
| verification proportionality | `references/collaboration/verification.md` |
| project architecture | `references/project/architecture.md` |
| project governance / artifact admission / drift | `references/project/governance.md` |
| normal resume / `CURRENT.md` | `references/project/current.md` |
| existing-project migration | `references/project/migration.md` |
| reports / layout | `references/project/reports.md` |
| explicit User-requested Concept | `references/project/concept.md` |
| current living Design | `references/project/design.md` |
| prior-art / reuse gate | `references/project/prior-art.md` |
| exceptional conversation handoff | `references/project/handoff.md` |
| first-party Skill development | `references/skill/development.md` |
| Skill writing / progressive disclosure | `references/skill/writing.md` |

Use one primary owner. Add a second owner only when the concern genuinely spans both responsibilities.

## Project state model

```text
reports/design/  = current accepted project design
reports/concept/ = explicit User-requested historical reasoning; append-only
CURRENT.md       = current work edge / NOW only
```

Project-specific canonical artifacts, scientific objects, source packages, and purity rules belong to the project that owns them, not to this generic collaboration Skill.

## Codex delegation

Every repository task delegated to Codex is committed under `reports/chatgpt/`; chat carries only the immutable locator.

```text
LOCAL-QUICK → bounded local work → compact result
FORMAL      → major/high-risk local work → reports/codex report → ChatGPT acceptance
```

Task prompts should specify the intended outcome, authority/boundaries, completion criteria, required evidence, and true decision boundary. Avoid command-by-command itineraries unless the commands themselves are the contract.

## Verification

Use the smallest evidence set that establishes the requested claim. Run broader or repeated checks only when risk, failures, new changes, or unresolved concerns justify them.

## Normal conversation resume

```text
AGENTS.md
→ CURRENT.md
→ reports/design/README.md when present
→ current owner only
```

When the User says `换对话框，给我提示词` or equivalent, return only the compact resume prompt owned by `project/current.md`.

## Cold paths

Do not preload Concept history, old tasks/reports/handoffs, archive, templates, or the full Design/reference tree. Load them only when the active concern requires them.
