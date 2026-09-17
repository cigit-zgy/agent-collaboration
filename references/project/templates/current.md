# Project CURRENT.md template

Cold path: load only when creating or materially restructuring repository-root `CURRENT.md`.

Current-work-state semantics are owned by `../current.md`.

## Goal

`CURRENT.md` is a tiny mutable pointer to the project's present work edge. It is not a history file.

Recommended shape:

```markdown
# Current project state

Status: <active | blocked | idle>
Updated: <YYYY-MM-DD or timestamp when useful>

## Work edge

<One or two sentences describing what is currently being worked on.>

## Active coordinates

- Branch: <branch when useful>
- ChatGPT task/record: <path when useful>
- Codex report: <path when useful>
- Relevant Design/Skill owner: <path when useful>
- Latest handoff: <reports/handoff/... when a conversation switch created one>

## Open edge

- <0–3 unresolved blockers/decisions only>

## Next action

<Exactly one directly executable next step.>
```

Remove unnecessary fields rather than filling `NONE` ceremony.

Do not copy Design semantics, project architecture, completed-task history, test summaries, old commits, Concept chronology, rejected alternatives, transcript, or long rationale into CURRENT.

When work advances, rewrite CURRENT to NOW. History belongs to Git and append-only Reports.

Target <= 4 KiB.

Fresh conversation without handoff:

```text
AGENTS.md → CURRENT.md → one current owner
```

Fresh conversation with a handoff pointer:

```text
AGENTS.md → CURRENT.md → that exact handoff → one current owner
```

Do not preload historical Reports or the whole Design tree.
