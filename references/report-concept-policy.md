# Report and concept asset policy

This file is the current operational authority for collaboration reports and durable
decision-history assets.

## Stable report layout

Each owning repository uses stable paths:

```text
reports/
├── chatgpt/
│   └── YYMMDD_chatgpt_NN.md
├── codex/
│   └── YYMMDD_codex_NN.md
└── concept/
    ├── README.md
    └── <stable-topic>.md
```

Create a directory only when its first owned artifact exists. Git does not require
empty report folders.

## Report immutability and lifecycle

A committed formal task or Codex report is an audit artifact. After issue:

- keep its repository-relative path stable;
- do not move it into calendar-based archives;
- do not rewrite the body merely to mark it closed;
- do not change a task after Codex has executed the committed task source;
- rely on Git history and report metadata for chronology and provenance.

Calendar-based weekly archive folders are not part of this policy.

If a task is superseded before execution, a new task may explicitly supersede it;
retain the original artifact unchanged. If lifecycle status needs to be tracked after
issue, use the paired report/verdict and Git history rather than mutating the original
formal specification.

## ChatGPT task metadata

Every new task begins with compact YAML front matter:

```yaml
---
artifact_type: chatgpt_task
task_id: 260902_chatgpt_04
title: <SHORT_TITLE>
status: issued
date: 2026-09-02
repository: cigit-zgy/agent-collaboration
branch: master
baseline_sha: <BASELINE_SHA>
verification_level: level_1
summary: >
  <ONE-TO-THREE-SENTENCE PURPOSE/SCOPE>
tags:
  - <TAG>
concepts: []
codex_report: reports/codex/260902_codex_04.md
---
```

Use metadata for identity/retrieval once. Do not repeat task ID, date, repository,
branch, baseline, status, or verification level as a second metadata block in the
body.

Do not put the task-source commit SHA inside the task itself because that would be
self-referential.

## Codex report metadata

Every new Codex report begins with:

```yaml
---
artifact_type: codex_report
task_id: 260902_chatgpt_04
title: <SHORT_TITLE>
verdict: PASS_WITH_LIMITATIONS
date: 2026-09-02
repository: cigit-zgy/agent-collaboration
branch: master
task_source_sha: <TASK_SOURCE_SHA>
baseline_sha: <BASELINE_SHA>
verification_level: level_1
summary: >
  <ONE-TO-THREE-SENTENCE IMPLEMENTATION/RESULT SUMMARY>
tags:
  - <TAG>
concepts: []
limitations: []
---
```

Do not repeat these identity fields as a second header block in the body. Do not put
the commit containing the report inside that same report; Git history and final
stdout own that value.

## Concept role

`references/*` is the current operational-policy layer.

`reports/concept/*` records accepted decision history and rationale. A concept file
must point to the current operational authority for its topic and must not duplicate
the complete current policy.

Concepts are useful for questions such as:

- Why was this architecture chosen?
- What did this policy supersede?
- Which alternatives were rejected?
- Which operational reference now owns the decision?

Concepts are not part of the ordinary Skill runtime path.

## Concept index

`reports/concept/README.md` is an index for historical design retrieval, not a runtime
router. Recommended fields:

```markdown
| ID | File | Topic | Status | Updated | Operational authority |
|---|---|---|---|---|---|
```

Read it only when design history or rationale is materially needed.

## Concept metadata and body

Use compact metadata:

```yaml
---
id: 04
title: Skill package architecture decisions
status: active
created: 2026-09-02
updated: 2026-09-02
role: decision_history
operational_authority:
  - references/skill-package-architecture.md
  - references/skill-repository-policy.md
related_tasks: []
---
```

Recommended body:

```markdown
# <Topic>

## Decision record

### <YYYY-MM-DD> — <short decision title>

- Decision: <accepted design choice>
- Rationale: <why>
- Supersedes/changes: <prior assumption if any>
- Operational authority: `<references/...>`
- Related tasks: <task IDs or none>
```

Add entries only for mature decisions that materially affect future architecture,
workflow, semantics, trust boundaries, or release/validation policy. Do not copy the
current reference text into a `Current conclusion` section.

## What belongs where

```text
references/*
= current operational contract

reports/concept/*
= decision history/rationale

reports/chatgpt/*
= immutable committed execution specification

reports/codex/*
= execution/verification evidence
```

Do not store transcripts, raw logs, routine test output, temporary hypotheses, or
project-specific truth from another repository in this repository's concept folder.
