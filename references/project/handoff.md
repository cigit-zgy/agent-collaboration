# Conversation-handoff contract

Load this reference when the User explicitly ends/replaces a long conversation (`换对话框`, `给我新对话框提示词`, or equivalent), or when a prior handoff is the explicit resume anchor.

## Purpose

A handoff is a compact conversation-boundary record. It exists so a full/long conversation can be replaced without reloading project history.

```text
Design   = current accepted semantics
Reports  = historical work/evidence
CURRENT  = NOW pointer
Handoff  = compact boundary between two conversations
```

A handoff never overrides current Design, task, scientific source, or repository state.

## Conversation-close lifecycle

When the User explicitly switches conversation:

```text
1. make accepted Design changes durable in the current owner;
2. ensure material ChatGPT/Codex/Concept records are committed;
3. reconcile Design if the backstop trigger in reconciliation.md is due;
4. rewrite CURRENT.md to the actual NOW edge;
5. create one NEW reports/handoff/YYMMDD_handoff_NN.md;
6. commit/push;
7. return only the compact resume prompt.
```

Do not overwrite an older handoff.

## Content contract

Target `<= 2 KiB`.

Record only:

```text
conversation time/range
ChatGPT report range touched in this conversation
Codex report range touched in this conversation
Concept range when any was explicitly created/used
current work edge
active branch/task/report coordinates when needed
0–3 unresolved edges
exactly one next action
```

Use report paths/ranges rather than copying report bodies.

Do not reproduce project overview, Design bodies, scientific background, test matrices, commit history, completed-task narrative, previous handoffs, or transcript text.

## Recovery

A new conversation normally reads:

```text
AGENTS.md
→ CURRENT.md
→ the exact handoff CURRENT points to
→ one directly relevant current owner as needed
```

Do not chain through older handoffs or preload historical Reports.

## User shorthand

When the repository is known, after the handoff has been committed return only:

```text
继续 cigit-zgy/<repository>。

按 AGENTS.md → CURRENT.md 恢复当前工作；
仅读取 CURRENT.md 指向的 handoff：reports/handoff/<THIS_FILE>。
不要预读其他历史。
```

No project recap or handoff body is pasted into chat.

## Completion

A handoff is sufficient when the next conversation can locate the current edge and one next action from `AGENTS.md + CURRENT.md + one handoff` while all durable semantics/evidence remain in their true owners.
