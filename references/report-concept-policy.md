# Report and concept asset policy

This policy defines the durable project-report layout used by the
ChatGPT ↔ Codex collaboration workflow.

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

Do not put transient run logs, scratch notes, raw test output, or Codex execution
history in `reports/concept/`.

Existing projects may retain legacy report directories. New work follows this
layout; do not rename historical reports merely for cosmetic consistency unless a
specific migration task requires it.

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

Continue updating the same topic file while the subject remains the same. Do not
create a new file for every discussion. Split a file only when the topic becomes a
separate durable contract with its own scope and consumers.

`reports/concept/README.md` is the authoritative index. Agents should inspect the
index first and read only concept files relevant to the current task.

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

Dates are durable decision checkpoints, not daily logs. Add a dated section only
when a discussion changes or materially clarifies project truth.

## Current truth and history

The latest non-deprecated dated decision in a topic is authoritative unless the
file explicitly states otherwise. Preserve earlier dated decisions as concise
history rather than rewriting the past to look internally consistent.

When a decision is superseded:

1. add a new dated section explaining the replacement;
2. update front-matter `updated`;
3. update `status` or `supersedes` where appropriate;
4. update `reports/concept/README.md`;
5. update related task IDs when an implementation task exists.

Do not duplicate the same rule in several concept files. One topic owns the rule;
other topics link to it.

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

A formal task may cite concept files as authoritative sources. A Codex report may
reference them but must not silently redefine them.
