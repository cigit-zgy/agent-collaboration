# Project current-work-state contract

Load this reference for repository-root `CURRENT.md`, normal multi-conversation resume, current work-edge ownership, or startup-context discipline.

Current accepted design is owned by `design.md`. Historical design reasoning is owned by `concept.md`. Exceptional conversation-only delta is owned by `handoff.md`. Existing-project policy migration is owned by `migration.md`.

## Purpose

A long-running project needs one cheap answer to:

```text
What are we working on now, and what should the next conversation do first?
```

Use exactly one repository-root:

```text
CURRENT.md
```

when the project regularly spans multiple ChatGPT/Codex sessions or when recovering the active work edge from repository state would otherwise be unnecessarily expensive.

`CURRENT.md` is current mutable work state. It is not design authority, task authority, execution evidence, history, or a conversation transcript.

## Authority relationship

```text
AGENTS.md
= project constitution / authority map

design/
= current accepted design

CURRENT.md
= current work edge + pointers only

reports/concept/
= historical design thinking

reports/chatgpt/
= durable Codex task specifications

reports/codex/
= FORMAL Codex execution evidence

reports/handoff/
= exceptional conversation-only delta
```

If `CURRENT.md` conflicts with current design, a committed task, scientific source authority, or actual repository state, the owning current authority/state wins and `CURRENT.md` must be corrected.

## Single-current-state invariant

A project using this model has exactly one root `CURRENT.md`.

Do not create:

```text
CURRENT_old.md
CURRENT_v2.md
CURRENT_20260910.md
current/
session_state/
conversation_01.md
conversation_02.md
```

merely to preserve earlier work states. Git history and the proper historical/task owners already preserve history.

## Content boundary

`CURRENT.md` should contain only information needed to orient the next session to the present work edge.

Useful fields are:

```text
status / updated timestamp
current work edge
active branch / task / report coordinates when relevant
directly relevant current design or Skill owners
at most a few unresolved blockers/decisions
one next action
```

It must not become:

```text
project architecture documentation
design semantics
chronological progress diary
completed-task catalogue
full test results
Codex report summary archive
concept history
rejected alternatives
commit log
backlog database
conversation transcript
```

Point to the owning artifact instead of copying it.

## Size discipline

Normal target:

```text
CURRENT.md <= 4 KiB
```

Above roughly 8 KiB, review whether history, design, task/report detail, or multiple unrelated work streams have leaked into the file. Reduce by moving information to its real owner and keeping only the pointer/current consequence.

These are architecture signals, not parser limits.

## Update lifecycle

`CURRENT.md` is overwritten as the active work edge changes.

At a meaningful work checkpoint:

```text
accepted design change          → update design/ first
important design rationale      → append reports/concept/ when useful
Codex task/report evidence      → keep in its task/report owner
repository state                → commit/push normally
current work edge               → rewrite CURRENT.md to NOW
```

Do not append a dated section merely to preserve what CURRENT used to say.

A repository-changing task that materially advances the active work edge should leave `CURRENT.md` consistent with the pushed state when the project uses this contract, unless the task explicitly stops at an isolated branch whose result is not yet adopted. In that case CURRENT points to the branch/report and states the unresolved adoption edge without pretending the result is current default-branch truth.

## Normal conversation resume

Routine replacement of a full ChatGPT conversation is **conversation resume**, not project migration.

Default orientation is:

```text
AGENTS.md
→ CURRENT.md
→ design/README.md when the project uses explicit living design
```

This orientation identifies the current concern; it does not require reading every file those documents mention.

Then use just-in-time retrieval:

```text
current concern
→ one directly relevant design topic when needed
→ workflow Skill/reference when execution requires it
→ exact active task/report when CURRENT points to it
→ exact concept note only when historical rationale is needed
```

Do not preload:

```text
all design topics
reports/concept/
old reports/chatgpt/
old reports/codex/
old reports/handoff/
00_archive/
complete collaboration references
```

Before the first substantive repository-changing ChatGPT write, resolve current collaboration authority once under `../collaboration/protocol.md`. This refresh requirement does not justify loading unrelated collaboration owners during orientation.

## Old-conversation closure

When a conversation is being retired because it is full:

```text
1. finish or safely checkpoint the current atomic work;
2. make accepted design/session state repository-native in the correct owner;
3. ensure active task/report/branch coordinates are durable;
4. rewrite CURRENT.md to the actual current work edge;
5. create a handoff only if meaningful residual conversation-only delta would otherwise be lost;
6. end the conversation without producing a project-wide prose recap.
```

A normal conversation switch should not trigger migration assessment, design reconstruction, or historical report review.

## New-conversation bootstrap

The User-facing bootstrap should normally be a short locator, ideally <= 1 KiB. A sufficient pattern is:

```text
Continue <OWNER/REPOSITORY>.
This is conversation resume, not project migration.
Recover from AGENTS.md → CURRENT.md → design/README.md.
Load only the current concern just in time; do not preload history.
```

After recovery, the assistant should respond compactly and continue the current next action. Do not reprint a large project summary merely to demonstrate that recovery succeeded.

## Startup-context target

Before the current concern is identified, the normal project-text read set is only:

```text
AGENTS.md
+ CURRENT.md
+ design/README.md when present
```

Approximately 10–12 KiB total is a useful target for mature projects; exceeding roughly 16 KiB before useful work begins is a routing smell that should prompt ownership/index simplification rather than a larger handoff.

## When CURRENT.md is unnecessary

Do not create `CURRENT.md` for a small/single-session repository where the active work state is obvious and there is no meaningful resume cost.

Create it when one or more are true:

```text
project regularly spans multiple conversations
active work edge is not obvious from default branch alone
several design/task artifacts exist but only a small subset is currently active
resume repeatedly costs substantial context or search
```

## Concurrency boundary

This contract optimizes sequential conversation replacement.

If genuinely concurrent, long-lived work streams later require independent mutable ownership, design that concurrency explicitly. Do not preemptively create per-conversation state files, and do not turn `CURRENT.md` into a session registry/history database.

## Completion

The current-state layer is healthy when a fresh conversation can determine the present work edge and first next action from `AGENTS.md + CURRENT.md + design/README.md` without loading project history, and CURRENT remains a small pointer-first representation of NOW.
