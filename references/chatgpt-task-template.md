# ChatGPT formal task template

Formal Codex tasks live under stable paths:

```text
reports/chatgpt/YYMMDD_chatgpt_NN.md
```

Do not create a Codex task until ChatGPT can name the concrete local/unavailable
capability that requires Codex.

## YAML metadata

Use identity/retrieval metadata once:

```yaml
---
artifact_type: chatgpt_task
task_id: <TASK_ID>
title: <SHORT_TITLE>
status: issued
date: <YYYY-MM-DD>
repository: <OWNER/REPOSITORY>
branch: <BRANCH>
baseline_sha: <BASELINE_SHA>
verification_level: <level_1 | level_2 | level_3>
summary: >
  <ONE-TO-THREE-SENTENCE PURPOSE/SCOPE>
tags:
  - <TAG>
concepts: []
codex_report: reports/codex/<YYMMDD_codex_NN.md>
---
```

Rules:

- do not store the task-source commit SHA inside the task itself;
- do not repeat metadata fields in the body;
- `concepts` contains only decision-history topics materially relevant to why the
  task exists; operational authority should be listed under `Authoritative sources`;
- after Codex executes the committed task source, do not mutate or move this task.

## Body template

```markdown
# <Task title>

## Mission

## Why Codex is required

<State the concrete local/unavailable capability. If none exists, do not issue the task.>

## Current evidence / diagnosed problem

## Authoritative sources

<List the current operational references/contracts and exact repository artifacts.>

## Scope

## Required changes

## Non-goals

## Scientific / product boundaries

## Engineering constraints

## Verification

## Acceptance criteria

## Git requirements

Follow `references/protocol.md` unless the task explicitly states a stricter
repository-specific rule.

## Codex report

Expected path: `reports/codex/YYMMDD_codex_NN.md`

## Final stdout

<Exact fixed stdout format.>
```

Before authoring, ChatGPT inspects the current repository/evidence and resolves every
design decision that can reasonably be resolved remotely. Required changes and
acceptance criteria must be directly checkable. Avoid open-ended instructions such
as “improve as much as possible.”

Commit and push the task before handoff. Codex treats that committed task source as
the specification; chat additions do not silently supersede it.
