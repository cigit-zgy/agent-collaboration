# Project current-work-state contract

Load this reference for repository-root `CURRENT.md`, normal multi-conversation resume, current work-edge ownership, or startup-context discipline.

Current accepted design lives under `reports/design/` and is owned by `design.md`. Explicit User-requested design history lives under `reports/concept/` and is owned by `concept.md`. Project governance drift/admission is owned by `governance.md`.

## Purpose

A long-running project needs one cheap answer to:

```text
What are we working on now, and what should the next conversation do first?
```

Use one repository-root `CURRENT.md` when the project spans multiple sessions or resume would otherwise be expensive.

`CURRENT.md` is mutable NOW-state. It is not design authority, task authority, scientific evidence, history, backlog, or transcript.

## Content contract

Keep only:

```text
status / updated timestamp
current work edge
active branch / task / report coordinates when relevant
directly relevant reports/design/ or Skill owners
0–3 unresolved blockers/decisions
one next action
```

Target `<= 4 KiB`. Above `8 KiB` is non-conforming unless an explicit project authority justifies it; move leaked design/science/evidence/history/backlog content to its owner.

Do not append dated progress. Rewrite CURRENT to represent NOW.

## Update lifecycle

At a meaningful checkpoint:

```text
accepted design change          → update reports/design/
explicit User request for Concept → create new dated Concept + update reports/design/ in the same work unit
Codex evidence                  → task/report owner
scientific/model evidence       → scientific/model/golden owner
current work edge               → rewrite CURRENT.md
```

Do not create Concept merely because rationale or execution evidence seems worth preserving; `concept.md` requires explicit User instruction.

## Normal conversation resume

Routine replacement of a full conversation is conversation resume, not project migration.

```text
AGENTS.md
→ CURRENT.md
→ reports/design/README.md when explicit living design is used
```

Then retrieve just in time only the directly relevant current owner, Skill/reference, or exact active task/report.

Do not preload the whole design tree, Concepts, old tasks/reports/handoffs, archive, or collaboration references.

Before the first substantive repository-changing write, resolve current collaboration authority once and apply the bounded governance conformance gate from `governance.md`. Deterministic governance drift is repaired before the new work expands it; scientific/design ambiguity returns to User + ChatGPT.

## User shorthand

When the User says `换对话框，给我提示词` or equivalent and the repository is known, return only:

```text
继续 cigit-zgy/<repository>。

这是 conversation resume，不执行 project migration。
按 AGENTS.md → CURRENT.md → reports/design/README.md 恢复当前工作。

只按 CURRENT.md 的 current work edge 按需读取相关 design / Skill / task / report；
不要预读历史。
```

Do not add recovery theory or project history unless explicitly requested.

## Old-conversation closure

When retiring a full conversation:

```text
finish/safely checkpoint the atomic work
→ make accepted state durable in its real owner
→ ensure active task/report/branch coordinates are durable
→ rewrite CURRENT.md to NOW
→ create handoff only for unavoidable residual conversation-only delta
→ end without project-wide recap
```

A normal switch does not trigger project migration or historical review.

## Startup-context target

Before identifying the current concern, normal project text is only:

```text
AGENTS.md + CURRENT.md + reports/design/README.md
```

If a fresh conversation cannot locate the current work and first next action from this small set, simplify routing/state ownership rather than adding a larger handoff.
