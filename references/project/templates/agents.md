# Project AGENTS.md template

Keep project `AGENTS.md` concise and scope-local. It identifies authority and owners; it does not reproduce workflow manuals.

````markdown
# <PROJECT_NAME> context

## Authority

```text
explicit User instruction
→ reports/design/                  current accepted Design when used
→ <workflow>/SKILL.md + references operational workflow
→ <implementation paths>          implementation
→ tests                           maintained verification logic
→ <source/evidence owner>         domain/scientific facts when applicable
```

`CURRENT.md` is NOW-state/navigation only.
`reports/chatgpt/`, `reports/codex/`, `reports/concept/`, and `reports/handoff/` are append-only historical records and never override current Design.

Global collaboration authority:
`cigit-zgy/agent-collaboration@<REVISION>`

## Ownership

```text
CURRENT.md          current work edge / next action
reports/design/     one current living Design set
reports/chatgpt/    ChatGPT durable work records
reports/codex/      Codex execution records
reports/concept/    explicit User-requested Concept history
reports/handoff/    conversation-boundary handoffs
<path>              <project-specific owner>
```

Current Skill profile owner:
`reports/design/<RUNTIME_AND_SKILLS_OWNER>.md` when the project uses multiple reusable Skills.

## Workflow

Normal resume:

```text
AGENTS.md
→ CURRENT.md
→ one directly relevant current owner
```

When CURRENT points to a handoff, read that one handoff before the current owner. Do not preload historical Reports.

Routine execution enters the relevant project Skill/reference directly.

## Design maintenance hook

Before substantive project work, perform the cheap Design-reconciliation trigger check defined by current `agent-collaboration/references/project/reconciliation.md`:

```text
inspect reports/design/README.md reconciliation cursor
→ inspect only new report filenames/metadata needed for the trigger check
→ if <4 new substantive reports, <7 days, and no design_gap/design_drift signal: continue normally
→ otherwise reconcile only reports newer than the cursor before continuing
```

Do not run repository-wide background/scheduled reconciliation. If this project is not being worked on, nothing happens.

An accepted Design consequence discovered during the current work is updated immediately in its one current Design owner; do not wait for the next reconciliation check.

Inside authorized reversible work, infer routine implementation details and continue through repair/verification. Ask only when the missing choice changes scientific/product meaning or another explicit project checkpoint.

## Hard boundaries

- `reports/design/` is the only current Design tree unless this repository explicitly declares the self-hosting Skill exception.
- Every current Design concern has one owner; no superseded/refining duplicate current topics.
- Historical ChatGPT/Codex/Concept/Handoff records are append-only.
- Every Codex repository task has a committed ChatGPT task and a durable Codex record.
- ChatGPT creates Concept only when the User explicitly requests Concept persistence.
- `CURRENT.md` represents NOW only and points to the latest handoff when a conversation switch created one.
- Scientific/model facts stay with their project-declared source/evidence owners.
- <project-specific hard boundary>
````

Do not copy global collaboration manuals, detailed test recipes, task history, Design bodies, Concept history, verification logs, or Skill manuals into `AGENTS.md`.
