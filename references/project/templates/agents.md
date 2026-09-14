# Project AGENTS.md template

Keep project `AGENTS.md` concise and scope-local. It identifies authority and owners; it does not reproduce workflow manuals.

````markdown
# <PROJECT_NAME> context

## Authority

```text
explicit User instruction
→ reports/design/                  current accepted Design
→ <workflow>/SKILL.md + references operational workflow
→ <implementation paths>          implementation
→ tests                           evidence
→ <source/evidence owner>         domain/scientific facts when applicable
```

`CURRENT.md` is NOW-state/navigation only.
`reports/concept/` is historical and created only when the User explicitly requests Concept persistence.

Global collaboration authority:
`cigit-zgy/agent-collaboration@<REVISION>`

## Ownership

```text
CURRENT.md          current work edge / next action
reports/design/     current living Design
reports/chatgpt/    durable Codex tasks
reports/codex/      FORMAL execution evidence
reports/concept/    explicit User-requested history
<path>              <project-specific owner>
```

## Workflow

Normal resume:

```text
AGENTS.md → CURRENT.md → reports/design/README.md → current owner
```

Routine execution enters the relevant project Skill/reference directly. Do not preload history or unrelated Design topics.

Inside authorized reversible work, infer routine implementation details and continue through repair/verification. Ask only when the missing choice changes scientific/product meaning or another explicit project checkpoint.

## Hard boundaries

- `reports/design/` is the only current Design tree when explicit Design is used.
- Project-specific scientific/canonical-artifact rules stay with the project that owns them.
- Every Codex repository task is committed under `reports/chatgpt/` before delegation.
- <project-specific hard boundary>
````

Do not copy global collaboration manuals, detailed test recipes, task history, Design bodies, Concept history, or verification logs into `AGENTS.md`.
