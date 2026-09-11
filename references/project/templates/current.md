# Project CURRENT.md template

Cold path: load this file only when creating or materially restructuring repository-root `CURRENT.md`.

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

- Branch: <branch | NONE>
- ChatGPT task: <path | NONE>
- Codex report: <path | NONE>
- Relevant design: <one or a few reports/design/... paths | NONE>
- Relevant workflow owner: <path | NONE>

## Open edge

- <0–3 unresolved blockers/decisions only>

## Next action

<One directly executable next step.>
```

Remove unnecessary fields rather than filling `NONE` ceremony.

Do not copy full design semantics, project architecture, completed-task history, test summaries, old commits, concept chronology, rejected alternatives, transcript, or long rationale into CURRENT.

When work advances, rewrite CURRENT to NOW. History belongs to Git and its proper owners.

Target <= 4 KiB. Above ~8 KiB, move leaked history/design/evidence to its owner.

A fresh conversation should recover through:

```text
AGENTS.md
→ CURRENT.md
→ reports/design/README.md
```

and know what to load next without reading historical reports or the whole design tree.
