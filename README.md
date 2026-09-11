# agent-collaboration

Reusable operating contracts for User ↔ ChatGPT ↔ Codex collaboration.

Repository state is durable memory; conversations are disposable working memory.

## Runtime entry

```text
AGENTS.md
→ SKILL.md
→ one primary owner
→ optional second owner only when genuinely needed
```

## Project governance layout

For long-running projects using explicit living design:

```text
CURRENT.md
= what we are working on now
= tiny mutable NOW-state / resume pointer

reports/
├── design/      what we currently accept; current living design authority
├── concept/     how we thought; historical design input
├── chatgpt/     durable Codex task specifications
├── codex/       FORMAL Codex execution evidence
└── handoff/     exceptional conversation-only residual delta
```

`reports/design/` is not a chronological report family. It uses `README.md`, optional `00_overview.md`, and dynamic `NN_<topic>.md` files under `project/design.md`.

The dated flat-report rules apply only to `chatgpt`, `codex`, `concept`, and `handoff`.

## Normal conversation resume

```text
AGENTS.md
→ CURRENT.md
→ reports/design/README.md
→ identify current concern
→ load only directly relevant owner(s) just in time
```

A full conversation does not trigger project migration and normally does not create a handoff.

`CURRENT.md` should stay pointer-first and small. `reports/handoff/` is used only for meaningful conversation-only delta that cannot reasonably live elsewhere.

## Project design model

```text
reports/concept/
= what we considered
= historical design reasoning/input
= never current authority

reports/design/
= what we currently accept
= one current structured design set
= dynamic topic decomposition
```

A material concept changes current authority only after User + ChatGPT adjudication updates `reports/design/`.

## Existing-project migration

Older repositories using root `design/` migrate that one current tree to:

```text
reports/design/
```

without rewriting project-specific scientific/product semantics.

Opening a new conversation does not by itself justify migration.

## Codex task model

Every repository task delegated to Codex is committed first under:

```text
reports/chatgpt/YYMMDD_chatgpt_NN.md
```

Then chat carries only the short locator.

```text
LOCAL-QUICK → task → compact result → no reports/codex report
FORMAL      → task → reports/codex report → ChatGPT acceptance/integration
```

Repository-changing Codex work must fresh-fetch and prove exact authorized remote/local equality before mutation and again after push.

## Context discipline

HOT:

```text
project AGENTS.md
CURRENT.md when used
reports/design/README.md when present
SKILL.md when collaboration routing is needed
```

WARM: directly relevant current design/Skill/task/report owner.

COLD: concept history, historical tasks/reports, handoffs unless explicitly relevant, `00_archive/`, unrelated owners/templates.

## Core principle

```text
repository carries continuity
reports/design carries current design
reports/concept carries design history
CURRENT.md carries only NOW
handoff carries only exceptional residual delta
```
