# Project current-work-state contract

Load this reference for repository-root `CURRENT.md`, normal multi-conversation resume, current work-edge ownership, or startup-context discipline.

Current accepted design is owned by `design.md` and lives under `reports/design/`. Historical design reasoning is owned by `concept.md` under `reports/concept/`. Exceptional conversation-only delta is owned by `handoff.md`. Existing-project policy migration is owned by `migration.md`.

## Purpose

A long-running project needs one cheap answer to:

```text
What are we working on now, and what should the next conversation do first?
```

Use exactly one repository-root `CURRENT.md` when the project regularly spans multiple sessions or resume would otherwise be expensive.

`CURRENT.md` is mutable NOW-state. It is not design authority, task authority, execution evidence, history, or transcript.

## Authority relationship

```text
AGENTS.md          = project constitution / authority map
reports/design/    = current accepted design
CURRENT.md         = current work edge + pointers only
reports/concept/   = historical design thinking
reports/chatgpt/   = durable Codex task specifications
reports/codex/     = FORMAL Codex execution evidence
reports/handoff/   = exceptional conversation-only delta
```

If CURRENT conflicts with current design, task authority, scientific source authority, or actual repository state, the owning authority/state wins and CURRENT must be corrected.

## Single-current-state invariant

Use one root `CURRENT.md`. Do not create `CURRENT_old.md`, dated CURRENT copies, `current/`, `session_state/`, or per-conversation state files merely to preserve history.

## Content boundary

Keep only:

```text
status / updated timestamp
current work edge
active branch / task / report coordinates when relevant
directly relevant reports/design/ or Skill owners
0–3 unresolved blockers/decisions
one next action
```

Do not copy project architecture, design semantics, chronological progress, completed-task catalogues, test results, report summaries, concept history, rejected alternatives, commit logs, backlogs, or transcripts. Point to the owner.

Target <= 4 KiB; above ~8 KiB, treat leakage as an architecture smell.

## Update lifecycle

At a meaningful checkpoint:

```text
accepted design change     → update reports/design/ first
important design rationale → append reports/concept/ when useful
Codex evidence             → task/report owner
repository state           → commit/push normally
current work edge          → rewrite CURRENT.md to NOW
```

Do not append dated history to CURRENT.

## Normal conversation resume

Routine replacement of a full conversation is **conversation resume**, not project migration.

Default orientation:

```text
AGENTS.md
→ CURRENT.md
→ reports/design/README.md when explicit living design is used
```

Then retrieve just in time:

```text
current concern
→ directly relevant reports/design topic when needed
→ workflow Skill/reference when needed
→ exact active task/report when CURRENT points to it
→ exact concept note only for historical rationale
```

Do not preload the whole design tree, reports/concept, old tasks/reports/handoffs, archive, or complete collaboration references.

Before the first substantive repository-changing ChatGPT write, resolve current collaboration authority once under `../collaboration/protocol.md`; that refresh does not justify unrelated preload.

## User shorthand — hard interaction rule

When the User says something equivalent to:

```text
换对话框，给我提示词
换个对话框
给我新对话框提示词
```

and the active repository is known, return only:

```text
继续 cigit-zgy/<repository>。

这是 conversation resume，不执行 project migration。
按 AGENTS.md → CURRENT.md → reports/design/README.md 恢复当前工作。

只按 CURRENT.md 的 current work edge 按需读取相关 design / Skill / task / report；
不要预读历史。
```

Do not add recovery theory or project history unless explicitly requested. If repository identity is genuinely ambiguous, ask only for that identity.

## Old-conversation closure

When retiring a full conversation:

```text
1. finish or safely checkpoint the current atomic work;
2. make accepted design/session state repository-native in the correct owner;
3. ensure active task/report/branch coordinates are durable;
4. rewrite CURRENT.md to the actual current work edge;
5. create a handoff only if meaningful residual conversation-only delta would otherwise be lost;
6. end without a project-wide prose recap.
```

A normal switch must not trigger migration assessment, design reconstruction, or historical report review.

## Startup-context target

Before identifying the current concern, the normal project-text set is:

```text
AGENTS.md
+ CURRENT.md
+ reports/design/README.md when present
```

Roughly 10–12 KiB is a useful mature-project target; >~16 KiB before useful work begins is a routing smell.

## When CURRENT.md is unnecessary

Do not create CURRENT for a small/single-session repository where active work is obvious. Use it when the project spans multiple conversations, has a non-obvious active edge, has many design/task artifacts with only a small active subset, or repeatedly incurs resume search/context cost.

## Concurrency boundary

This contract optimizes sequential conversation replacement. Do not preemptively create per-conversation state files or turn CURRENT into a session registry.

## Completion

The current-state layer is healthy when a fresh conversation can determine the present work edge and first next action from `AGENTS.md + CURRENT.md + reports/design/README.md` without loading history.
