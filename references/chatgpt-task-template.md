# ChatGPT formal task template

Formal tasks live under `reports/chatgpt/` and use:

```text
YYMMDD_chatgpt_NN.md
```

Use every field and section. Write `None` where a section genuinely has no
content; do not omit it.

```markdown
# <Task title>

Task ID: <TASK_ID>
Issued: <DATE>
Repository: <OWNER/REPOSITORY>
Local repository: <ABSOLUTE_LOCAL_REPOSITORY>
Branch: <BRANCH>
Baseline SHA: <BASELINE_SHA>
Verification level: <LEVEL 1 — FOCUSED | LEVEL 2 — MAJOR | LEVEL 3 — RELEASE>
Status: <STATUS>

## Mission

## Current evidence / diagnosed problem

## Authoritative sources

## Scope

## Required changes

## Non-goals

## Scientific / product boundaries

## Engineering constraints

## Verification

## Acceptance criteria

## Git requirements

State the branch/upstream expectations and any repository-specific exceptions.
Unless the task explicitly says otherwise, Codex must follow
`references/protocol.md` repository synchronization:

- fetch and inspect branch, `HEAD`, upstream, and worktree before editing;
- preserve pre-existing user changes;
- fast-forward only when safe; do not invent a merge/rebase for divergence;
- commit and push all task-scoped repository changes;
- fetch again and verify final `HEAD == upstream`;
- report any intentionally preserved non-task worktree changes.

## Codex report

Expected path: `reports/codex/YYMMDD_codex_NN.md`

## Final stdout
```

Before authoring the task, ChatGPT must inspect the current repository and
relevant artifacts. The task must state the actual baseline SHA and one
verification level. Required changes and acceptance criteria must be directly
checkable, and non-goals must bound the work. Do not use open-ended phrases such
as “improve as much as possible,” and do not pre-schedule the next task.

If the task changes a durable design decision, update the owning
`reports/concept/` topic before or as part of the committed task so Codex has a
stable authoritative contract.

Commit and push the task before handing it to Codex. Codex treats that committed
task as the sole specification; chat additions are not task authority.
