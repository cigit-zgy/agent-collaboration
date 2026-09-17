# Project current-work-state contract

Load this reference for repository-root `CURRENT.md`, normal multi-conversation resume, current work-edge ownership, or startup-context discipline.

Current accepted Design is owned by `design.md`; report history by `reports.md`; explicit conversation-boundary records by `handoff.md`; Design backstop synchronization by `reconciliation.md`.

## Purpose

`CURRENT.md` answers only:

```text
What are we working on now, and what should the next conversation do first?
```

Use one repository-root `CURRENT.md` when the project spans multiple sessions or resume would otherwise be expensive.

It is mutable NOW-state, not Design authority, task authority, scientific evidence, history, backlog, or transcript.

## Content contract

Keep only:

```text
status / updated timestamp
current work edge
active branch / task / report coordinates when relevant
directly relevant current Design or Skill owner
latest handoff path when a conversation switch created one
0–3 unresolved blockers/decisions
one next action
```

Target `<= 4 KiB`. Do not append dated progress; rewrite to NOW.

## Update lifecycle

At meaningful checkpoints:

```text
accepted Design change      → update current Design immediately
ChatGPT/Codex work          → append durable report when required
explicit Concept request    → new Concept + same-work-unit Design update when applicable
current work edge           → rewrite CURRENT.md
explicit conversation switch → create handoff and point CURRENT to it
```

Periodic reconciliation is a backstop, not a reason to delay an already-known Design update.

## Normal resume

Without a handoff:

```text
AGENTS.md
→ CURRENT.md
→ one directly relevant current owner
```

When CURRENT points to a conversation handoff:

```text
AGENTS.md
→ CURRENT.md
→ that exact handoff
→ one directly relevant current owner as needed
```

Do not preload the whole Design tree, Concepts, old tasks/reports/handoffs, archive, or collaboration references.

## User shorthand

When the User says `换对话框`, `给我新对话框提示词`, or equivalent and the repository is known:

```text
close the conversation under handoff.md
→ commit/push the new handoff and updated CURRENT
→ return only the compact prompt below
```

```text
继续 cigit-zgy/<repository>。

按 AGENTS.md → CURRENT.md 恢复当前工作；
仅读取 CURRENT.md 指向的 handoff：reports/handoff/<THIS_FILE>。
不要预读其他历史。
```

Do not add a prose project recap.

## Startup-context target

A fresh conversation should identify the current concern from:

```text
AGENTS.md + CURRENT.md + at most one current handoff
```

Then load only the relevant current Design/Skill/task/report owner just in time.

If this small set cannot identify the work edge and first next action, simplify ownership/routing rather than making CURRENT or Handoff larger.
