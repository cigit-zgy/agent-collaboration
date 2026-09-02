# Report and concept asset policy

This policy defines the durable project-report layout used by the ChatGPT ↔ Codex collaboration workflow.

## Directory ownership

Projects using this protocol should use:

```text
reports/
├── chatgpt/
│   └── YYMMDD_chatgpt_NN.md
├── codex/
│   └── YYMMDD_codex_NN.md
└── concept/
    ├── README.md
    ├── 00_project_concept.md
    ├── 01_<topic>.md
    ├── 02_<topic>.md
    └── ...
```

Ownership is strict:

- `reports/chatgpt/`: committed formal task specifications authored by ChatGPT.
- `reports/codex/`: Codex implementation, verification, limitation, and Git-state reports.
- `reports/concept/`: durable design decisions formed by the User and ChatGPT.

Do not put transient run logs, scratch notes, raw test output, or Codex execution history in `reports/concept/`.

Existing projects may retain legacy report directories. New work follows this layout; do not rename historical reports merely for cosmetic consistency unless a specific migration task requires it.

## Structured metadata for ChatGPT tasks

Every new `reports/chatgpt/*.md` task begins with YAML front matter. Its purpose is retrieval, filtering, and task/report linkage rather than duplicating the full task body.

Required fields:

```yaml
---
artifact_type: chatgpt_task
task_id: 260902_chatgpt_02
title: Harden global Git and verification policy
status: issued
date: 2026-09-02
repository: cigit-zgy/agent-collaboration
branch: master
baseline_sha: <BASELINE_SHA>
verification_level: level_1
summary: >
  Update global Git synchronization, verification tooling, environment reuse,
  and fast-development policy.
tags:
  - git-sync
  - verification
concepts:
  - 00_global_codex_policy
codex_report: reports/codex/260902_codex_02.md
---
```

Rules:

- `summary` is a compact one-to-three-sentence synopsis of purpose and scope.
- `tags` contains a small number of stable retrieval terms, not every noun in the task.
- `concepts` contains only durable concept assets that materially govern the task; use `[]` when none.
- `codex_report` records the expected paired Codex report path.
- do not store the task-source commit SHA inside the task itself; that commit contains the file and would create a self-reference problem.

## Structured metadata for Codex reports

Every new `reports/codex/*.md` report begins with YAML front matter:

```yaml
---
artifact_type: codex_report
task_id: 260902_chatgpt_02
title: Global Git and verification policy implementation
verdict: PASS_WITH_LIMITATIONS
date: 2026-09-02
repository: cigit-zgy/agent-collaboration
branch: master
task_source_sha: <TASK_SOURCE_SHA>
baseline_sha: <BASELINE_SHA>
verification_level: level_1
summary: >
  Applied the machine-global policy and verified Git synchronization and tool
  availability.
tags:
  - git-sync
  - verification
concepts:
  - 00_global_codex_policy
limitations:
  - semgrep-not-installed
---
```

Rules:

- `summary` describes actual implementation and resulting state, not planned work.
- `verdict` uses `PASS`, `PASS_WITH_LIMITATIONS`, `BLOCKED`, or `FAIL` in YAML.
- `limitations` contains only material non-blocking limitations; use `[]` when none.
- `task_source_sha` binds the report to the committed formal task.
- do not store the commit that contains the report inside that same report; Git history and final stdout own the final report commit SHA.

Task/report metadata is deliberately compact. Do not add authors, timestamps, hashes, counters, environment fingerprints, or other fields unless they have a current retrieval or provenance consumer.

## Concept model

Concept assets are organized by stable topic, not by conversation or task.

Use one file per durable topic:

```text
00_project_concept.md
01_skill_architecture.md
02_workspace_contract.md
03_data_contract.md
04_validation_protocol.md
```

Continue updating the same topic file while the subject remains the same. Do not create a new file for every discussion. Split a file only when the topic becomes a separate durable contract with its own scope and consumers.

`reports/concept/README.md` is the authoritative index. Agents should inspect the index first and read only concept files relevant to the current task.

Recommended index fields:

```markdown
| ID | File | Concept | Status | Updated | Scope |
|---|---|---|---|---|---|
| 00 | 00_project_concept.md | Project concept | active | 2026-09-02 | project-wide |
```

## Concept metadata

Each concept topic begins with compact YAML front matter:

```yaml
---
id: 02
title: Workspace Contract
status: active
created: 2026-08-29
updated: 2026-09-02
authority: project
scope: workspace initialization and lifecycle
supersedes: null
related_tasks:
  - 260902_chatgpt_01
---
```

Required metadata:

- `id`: stable numeric topic identifier matching the filename prefix;
- `title`: durable topic name;
- `status`: `active`, `frozen`, or `deprecated`;
- `created`: first decision date;
- `updated`: date of the latest durable change;
- `authority`: normally `project`;
- `scope`: one concise boundary statement;
- `supersedes`: prior concept ID/file when applicable, otherwise `null`;
- `related_tasks`: formal task IDs that materially implemented or changed the concept; use `[]` when none.

Do not add metadata merely because it might be useful later.

## Dated decision history

Within a concept file, maintain chronological decision sections using ISO dates:

```markdown
# Workspace Contract

## 2026-08-29

### Decision
<current decision introduced on this date>

### Rationale
<why this decision was made>

### Impact
<what contracts, Skills, or artifacts this affects>

### Related tasks
- 260829_chatgpt_01

## 2026-09-02

### Decision
<new or revised durable decision>

### Changes from previous state
<what changed; omit only when this is the first entry>

### Rationale
<why>

### Impact
<affected project areas>

### Related tasks
- 260902_chatgpt_01
```

Dates are durable decision checkpoints, not daily logs. Add a dated section only when a discussion changes or materially clarifies project truth.

## Current truth and history

The latest non-deprecated dated decision in a topic is authoritative unless the file explicitly states otherwise. Preserve earlier dated decisions as concise history rather than rewriting the past to look internally consistent.

When a decision is superseded:

1. add a new dated section explaining the replacement;
2. update front-matter `updated`;
3. update `status` or `supersedes` where appropriate;
4. update `reports/concept/README.md`;
5. update related task IDs when an implementation task exists.

Do not duplicate the same rule in several concept files. One topic owns the rule; other topics link to it.

## What belongs in concept

Record:

- accepted project purpose and boundaries;
- architecture decisions;
- interface and data contracts;
- scientific or product semantics;
- trust-state definitions;
- testing or release policy when it is project-specific;
- explicit changes to those decisions.

Do not record:

- conversational transcript;
- temporary hypotheses that were never accepted;
- routine test results;
- implementation details with no durable design consequence;
- Codex self-reported status;
- raw logs.

## Relationship to tasks and reports

```text
User + ChatGPT discussion
→ reports/concept/ durable decision when needed
→ reports/chatgpt/ committed implementation task
→ Codex implementation
→ reports/codex/ implementation evidence
→ ChatGPT independent audit
→ update concept only if acceptance establishes or changes durable project truth
```

A formal task may cite concept files as authoritative sources. A Codex report may reference them but must not silently redefine them.
