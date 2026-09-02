# Report and concept asset policy

This policy defines the durable project-report layout used by the User ↔ ChatGPT ↔
Codex collaboration workflow.

## Directory ownership

Each project using this protocol owns its own collaboration assets:

```text
reports/
├── chatgpt/
│   ├── YYMMDD_chatgpt_NN.md
│   └── archive/
│       └── YYMMDD/
│           └── <closed ChatGPT task files>
├── codex/
│   ├── YYMMDD_codex_NN.md
│   └── archive/
│       └── YYMMDD/
│           └── <closed Codex report files>
└── concept/
    ├── README.md
    ├── 00_project_concept.md
    ├── 01_<topic>.md
    ├── 02_<topic>.md
    └── ...
```

Ownership is strict:

- `reports/chatgpt/`: current or not-yet-archived formal task specifications authored
  by ChatGPT.
- `reports/chatgpt/archive/`: archived closed ChatGPT task specifications.
- `reports/codex/`: current or not-yet-archived Codex implementation reports.
- `reports/codex/archive/`: archived closed Codex implementation reports.
- `reports/concept/`: durable design conclusions formed by the User and ChatGPT.

Project report assets stay in the project that owns them. Do not centralize other
projects' reports inside the `agent-collaboration` repository.

Do not put transient run logs, scratch notes, raw test output, or Codex execution
history in `reports/concept/`.

Existing projects may retain legacy report directories. New work follows this
layout; do not rename historical reports merely for cosmetic consistency unless a
specific migration task requires it.

## Weekly report archive

Archive is lifecycle organization, not a duplicate backup. Git already preserves
historical versions.

Use independent archives under `chatgpt/` and `codex/`:

```text
reports/chatgpt/archive/260831/
reports/codex/archive/260831/
```

The archive folder name is the Monday that begins the completion week, formatted as
`YYMMDD`. For example, work completed during 2026-08-31 through 2026-09-06 belongs
under `260831/`.

Archive maintenance is normally performed about once per week. Do not create empty
weekly folders merely because a calendar week exists.

A task pair is eligible for archive only after:

1. ChatGPT issued the formal task;
2. Codex completed or terminated the task and wrote its report;
3. ChatGPT independently audited the result and issued the final verdict;
4. no further execution is expected under that task ID.

Unfinished, blocked-awaiting-decision, or still-active task/report files remain in
the root of their respective `chatgpt/` or `codex/` directory even when a new week
begins.

When archiving a closed pair:

1. use `git mv`, not copy-and-delete semantics that leave duplicate active files;
2. move the ChatGPT task to `reports/chatgpt/archive/<MONDAY_YYMMDD>/`;
3. move the Codex report to `reports/codex/archive/<MONDAY_YYMMDD>/`;
4. set the ChatGPT task metadata `status` to `closed` if it is not already closed;
5. update active repository-relative metadata links such as `codex_report` so they
   resolve to the archived location;
6. preserve task IDs, task-source SHAs, baseline SHAs, verdicts, summaries, and Git
   history unchanged.

Do not archive `reports/concept/` by week. Concept assets are long-lived project
knowledge, not execution-history batches.

## Structured metadata for ChatGPT tasks

Every new `reports/chatgpt/*.md` task begins with YAML front matter. Its purpose is
retrieval, filtering, and task/report linkage rather than duplicating the full task
body.

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
- `tags` contains a small number of stable retrieval terms, not every noun in the
  task.
- `concepts` contains only durable concept assets that materially govern the task;
  use `[]` when none.
- `codex_report` records the paired Codex report path and must be updated if the
  report is archived.
- do not store the task-source commit SHA inside the task itself; that commit
  contains the file and would create a self-reference problem.

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
- do not store the commit that contains the report inside that same report; Git
  history and final stdout own the final report commit SHA.

Task/report metadata is deliberately compact. Do not add authors, timestamps, hashes,
counters, environment fingerprints, or other fields unless they have a current
retrieval or provenance consumer.

## Concept model

Concept assets record mature stage conclusions and their evolution. They are
organized by stable topic, not by week, conversation, or implementation task.

Use one file per durable topic:

```text
00_project_concept.md
01_skill_architecture.md
02_workspace_contract.md
03_data_contract.md
04_validation_protocol.md
```

Continue updating the same topic file while the subject remains the same. Do not
create a new file for every discussion or every week. Split a file only when the
topic becomes a separate durable contract with its own scope and consumers.

`reports/concept/README.md` is the authoritative index. Agents inspect the index
first and read only concept files relevant to the current task.

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
- `created`: first durable conclusion date;
- `updated`: date of the latest durable conclusion change;
- `authority`: normally `project`;
- `scope`: one concise boundary statement;
- `supersedes`: prior concept ID/file when applicable, otherwise `null`;
- `related_tasks`: formal task IDs that materially implemented or changed the
  concept; use `[]` when none.

Do not add metadata merely because it might be useful later.

## Current conclusion and decision history

Every new concept topic uses two semantic layers:

```markdown
# Workspace Contract

## Current conclusion

<Concise authoritative statement of what the project currently accepts as true.>

## Decision history

### 2026-08-29

#### Conclusion
<Stage conclusion accepted on this date.>

#### Rationale
<Why it was accepted.>

#### Boundary
<What this conclusion covers and explicitly does not cover.>

#### Impact
<What contracts, Skills, interfaces, or artifacts it affects.>

#### Related tasks
- 260829_chatgpt_01

### 2026-09-02

#### Conclusion
<New or revised mature conclusion.>

#### Changes from previous conclusion
<Material delta from the prior accepted state.>

#### Rationale
<Why the change was accepted.>

#### Boundary
<Updated scope or exclusions.>

#### Impact
<Affected project areas.>

#### Related tasks
- 260902_chatgpt_03
```

`Current conclusion` is the authoritative fast-reading layer. Keep it concise and
update it in place when a mature decision changes.

`Decision history` preserves why the current conclusion evolved. Add a dated entry
only when User + ChatGPT reach a sufficiently mature stage conclusion that affects
future architecture, scientific/product semantics, interfaces, trust states,
workflow, validation, or another durable project contract. A weekly discussion
cadence may often produce such a checkpoint, but the calendar alone is not a reason
to create an entry.

Do not require an Agent to reconstruct current truth by reading all historical
entries. If history and `Current conclusion` disagree, `Current conclusion` is
current authority and the newest history entry should explain the change.

When a concept itself is superseded or deprecated, update front matter and the
concept index rather than moving it into weekly report archives.

## What belongs in concept

Record:

- accepted project purpose and boundaries;
- architecture decisions;
- interface and data contracts;
- scientific or product semantics;
- trust-state definitions;
- testing or release policy when it is project-specific;
- mature changes to those decisions.

Do not record:

- conversational transcript;
- temporary hypotheses that were never accepted;
- routine test results;
- implementation details with no durable design consequence;
- Codex self-reported status;
- raw logs.

## Relationship to tasks and reports

```text
User + ChatGPT discussion and design
→ reports/concept/ mature durable conclusion when needed
→ ChatGPT direct repository action when fully supported
OR
→ reports/chatgpt/ implementation-ready local task when Codex is required
→ Codex implementation
→ reports/codex/ implementation evidence
→ ChatGPT independent audit
→ update concept only if acceptance establishes or changes durable project truth
→ weekly git-move of closed task/report pairs into their own archives
```

A formal task may cite concept files as authoritative sources. A Codex report may
reference them but must not silently redefine them.
