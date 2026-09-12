# Project AGENTS.md template

Keep project `AGENTS.md` concise and scope-local. Route global collaboration behavior through current/pinned `agent-collaboration/SKILL.md`.

````markdown
# <PROJECT_NAME> context

## Authority

```text
explicit User instruction
→ reports/design/                  current accepted project Design
→ <workflow>/SKILL.md + references operational workflow
→ <implementation paths>          implementation
→ tests                           conformance evidence
→ <source/evidence owner>         model/domain scientific facts
```

`CURRENT.md` is NOW-state/navigation only.
`reports/concept/` is explicit User-requested historical design reasoning only.

Global collaboration authority:
`cigit-zgy/agent-collaboration@<REVISION>`

## Ownership

```text
CURRENT.md          current work edge / next action
reports/design/     one current living Design set
reports/chatgpt/    durable Codex tasks
reports/codex/      FORMAL execution evidence
reports/concept/    explicit User-requested Concept history
reports/handoff/    exceptional conversation-only delta
<path>              <project-specific owner>
```

## Workflow

Normal resume:

```text
AGENTS.md
→ CURRENT.md
→ reports/design/README.md
→ one directly relevant owner
```

Before the first substantive repository-changing ChatGPT write, apply the bounded governance conformance gate from current `agent-collaboration`.

Routine execution:

```text
AGENTS.md
→ <workflow>/SKILL.md
→ owning reference/script
```

## Hard invariants

- `reports/design/` is the only current Design tree.
- Every current Design concern has one owner; no superseded/refining duplicate current topics.
- Bounded work normally reads one primary Design owner plus at most one necessary secondary owner.
- ChatGPT creates a Concept only when the User explicitly requests Concept persistence.
- Every Concept request creates a NEW dated `reports/concept/YYMMDD_concept_NN.md`; existing Concepts are not overwritten.
- The same work unit also updates current `reports/design/` to the accepted consequence.
- Scientific/model facts and qualification/execution evidence remain with their scientific/task/report owners.
- `CURRENT.md` represents NOW only; target <=4 KiB and no project-history dump.
- Every Codex repository task is committed under `reports/chatgpt/` before delegation.
- <project-specific hard boundary>
````

Do not copy global manuals, task history, Design bodies, Concept history, or verification logs into `AGENTS.md`.
