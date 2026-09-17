# Codex record template

Every Codex repository task leaves one append-only record at:

```text
reports/codex/YYMMDD_codex_NN.md
```

`execution.md` owns the common requirement. FORMAL lifecycle is owned by `formal.md`.

A Codex record preserves execution evidence; it does not redefine Design or self-accept.

## Common metadata

```yaml
---
artifact_type: codex_report
artifact_id: <YYMMDD_codex_NN>
record_kind: <local_quick | formal>
task_id: <TASK_ID>
title: <SHORT_TITLE>
date: <YYYY-MM-DD>
project: <PROJECT_NAME>
repository: <OWNER/REPOSITORY>
status: completed
summary: >
  <IMPLEMENTATION/RESULT SUMMARY>
verdict: <PASS | PASS_WITH_LIMITATIONS | BLOCKED | FAIL>
task_source_sha: <TASK_SOURCE_SHA>
baseline_sha: <BASELINE_SHA when meaningful>
result_sha: <FINAL_PUBLISHED_SHA when meaningful>
design_topics: []
design_signal: <none | design_change | design_drift | design_gap>
limitations: []
---
```

Add branch/upstream/evidence coordinates only when they materially establish the result.

## LOCAL-QUICK body

Keep it compact:

```markdown
# <Task title> — Codex record

## Changes
<few bullets>

## Evidence
<focused checks only>

## Result
<final branch/SHA + limitations/blocker + Design signal>
```

The point is durable reconstructability, not a long narrative.

## FORMAL body

Use enough detail to establish the task's richer evidence claim:

```markdown
# <Task title> — Codex report

## Changes
## Material implementation choices / boundaries
## Verification evidence
## Limitations / blockers
## Repository publication state
## Design signal
```

For repository-changing work, record the final local and fetched remote coordinates needed to prove that the published state corresponds to the executed result. A publication mismatch cannot be reported as PASS.

## Design signal

```text
none           no current Design consequence
design_change  accepted result appears to require current Design update
design_drift   implementation/current owner conflicts with accepted Design
design_gap     current Design does not determine required semantics
```

ChatGPT performs acceptance and current Design synchronization under `formal.md` / `project/reconciliation.md`.

## Completion response

After the record-containing commit is published, Codex returns only the compact Result contract required by the task, including the report path and final repository coordinate when requested.
