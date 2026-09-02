# Report and concept asset policy

This file is the current operational authority for collaboration reports and project
concept assets.

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
body. Do not put the task-source commit SHA inside the task itself because that would
be self-referential.

## Codex report metadata

Every new Codex report begins with compact YAML front matter containing task/report
identity, source/baseline SHA, verification level, summary, tags, relevant concepts,
and material limitations. Do not repeat these identity fields as a second header
block in the body. Do not put the commit containing the report inside that same
report; Git history and final stdout own that value.

## Concept roles

A concept topic has one declared role. Do not blur the two roles below.

### `decision_history`

Use when the concept records accepted rationale, supersession, and why an operational
contract evolved. This is the role used by the `agent-collaboration` repository's own
`reports/concept/` topics.

For this role:

```text
references/*
= current operational authority

reports/concept/*
= decision history/rationale + pointer to current operational authority
```

The concept must not duplicate the complete current policy or override its owning
operational reference.

### `design_authority`

A maintained scientific/research project may explicitly declare selected
`reports/concept/*` topics as its canonical User + ChatGPT design specification.
This role is appropriate when the concept captures the complete accepted scientific,
architectural, trust, interface, or cross-stage design that downstream implementation
must realize.

For this role, separate concerns by level:

```text
Level 1  reports/concept/*
         canonical design specification: WHAT + WHY + accepted scientific/
         architectural semantics

Level 2  SKILL.md + references/
         operational projection: how an Agent routes and executes the design

Level 3  scripts / source code / schemas
         implementation

Level 4  tests/
         verification that the implementation/projection conforms

Level 5  workspace/data/runtime artifacts
         produced or mutable project state
```

`Level 2–5` must conform to `Level 1`. A Skill/reference may summarize, route, or
materialize a design-authority concept for execution, but it must not silently
reinterpret or supersede the governing design.

If a design-authority concept says `A`, an operational projection says `B`, and code
implements `C`, treat `B/C` as projection/implementation drift unless User + ChatGPT
explicitly approve a new design and update the governing concept first.

A project must declare this design-authority relationship in its root `AGENTS.md` and
concept index. Do not infer it merely because a `reports/concept/` directory exists.

## Scientific source authority remains separate

Design authority is not scientific source evidence.

For source-grounded scientific projects, keep these independent:

```text
project design truth
= declared design-authority concept topics

model/source scientific facts
= registered original source + evidence/provenance chain
```

A concept may define how evidence must be represented, validated, or promoted; it
must not invent a model-specific scientific value that the registered source does not
establish.

## Runtime versus design/audit reading

Design-authoritative concepts do not need to be loaded during every routine Agent run.
Use two reading modes.

Normal runtime:

```text
AGENTS.md
→ workflow SKILL.md
→ owning sub-Skill
→ required reference/script
```

Design, architecture change, implementation audit, or suspected drift:

```text
AGENTS.md
→ reports/concept/README.md
→ relevant design-authority concept topic(s)
→ affected SKILL/reference projection
→ implementation/tests as needed
```

This preserves progressive disclosure without weakening the project's canonical
design source.

## Concept index

`reports/concept/README.md` declares each topic's role and owner. Recommended fields:

```markdown
| ID | File | Topic | Role | Status | Updated | Operational projection/authority |
|---|---|---|---|---|---|---|
```

For `design_authority`, point to the downstream Skill/reference files that project the
design into operation. For `decision_history`, point to the current operational
authority.

## Concept metadata and body

### Design-authority topic

```yaml
---
id: 06
title: Trust state and artifact lifecycle
status: active
created: 2026-08-29
updated: 2026-09-02
role: design_authority
operational_projection:
  - water-bioprocess-agent/references/lifecycle-contract.md
related_tasks: []
---
```

Recommended body:

```markdown
# <Topic>

## Current design specification

<Complete current accepted design for this topic.>

## Decision history

### <YYYY-MM-DD> — <decision>
- Decision: ...
- Rationale: ...
- Changes/supersedes: ...
```

The `Current design specification` is authoritative for the declared topic. Update it
only through an explicit User + ChatGPT design decision.

### Decision-history topic

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
related_tasks: []
---
```

Keep a concise chronological decision record with rationale and pointers to the
current operational owner; do not duplicate the owner's full current text.

## What belongs where

The owning project declares which model applies. For a design-authoritative research
project, the normal relationship is:

```text
reports/concept/*  canonical project design specification
SKILL.md/references operational projection of that design
scripts/code/schema implementation
 tests/             conformance verification
workspace/          runtime/research artifacts
reports/chatgpt/*   immutable committed execution specifications
reports/codex/*     execution/verification evidence
```

For `agent-collaboration` itself, concepts remain `decision_history` and
`references/*` remain current operational policy.

Do not store transcripts, raw logs, routine test output, temporary hypotheses, or
another repository's project truth in concept assets.