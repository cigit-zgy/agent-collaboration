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
- Relevant design: <one or a few paths | NONE>
- Relevant workflow owner: <path | NONE>

## Open edge

- <0–3 unresolved blockers/decisions only>

## Next action

<One directly executable next step.>
```

Remove fields/sections that are unnecessary. Do not fill `NONE` ceremony when omission is clearer.

## Hard content rules

Do not copy into CURRENT:

```text
full design semantics
project architecture
completed-task history
full test/evidence summaries
old branch/commit catalogue
concept chronology
rejected alternatives
conversation transcript
long rationale
```

Use paths/coordinates and one current consequence instead.

## Rewrite rule

When work advances, rewrite CURRENT to represent the new NOW. Do not append dated progress entries.

Bad:

```text
2026-09-08: finished A
2026-09-09: finished B
2026-09-10: started C
```

Good:

```text
Current work edge: C
Relevant design: design/03_c.md
Next action: validate C against <owner>
```

## Size check

Target <= 4 KiB. Above ~8 KiB, stop adding content and move leaked history/design/evidence to its owning artifact.

## Resume quality check

A fresh conversation should be able to read:

```text
AGENTS.md
→ CURRENT.md
→ design/README.md
```

and know what to load next without reading historical reports or the whole design tree.
