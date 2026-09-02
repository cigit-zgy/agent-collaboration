# ChatGPT formal task template

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

## Agent report

## Final stdout
```

Before authoring the task, ChatGPT must inspect the current repository and
relevant artifacts. The task must state the actual baseline SHA and one
verification level. Required changes and acceptance criteria must be directly
checkable, and non-goals must bound the work. Do not use open-ended phrases such
as “improve as much as possible,” and do not pre-schedule the next task.

Commit and push the task before handing it to Codex. Codex treats that committed
task as the sole specification; chat additions are not task authority.
