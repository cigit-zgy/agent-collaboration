# Codex report template

Codex reports live at:

```text
reports/codex/YYMMDD_codex_NN.md
```

A report records execution evidence; it does not redefine project design or operational policy.

## Metadata

```yaml
---
artifact_type: codex_report
task_id: <TASK_ID>
title: <SHORT_TITLE>
verdict: <PASS | PASS_WITH_LIMITATIONS | BLOCKED | FAIL>
date: <YYYY-MM-DD>
repository: <OWNER/REPOSITORY>
branch: <BRANCH>
task_source_sha: <TASK_SOURCE_SHA>
baseline_sha: <BASELINE_SHA>
verification_level: <level_1 | level_2 | level_3>
summary: >
  <IMPLEMENTATION/RESULT SUMMARY>
tags: []
concepts: []
limitations: []
---
```

## Body

```markdown
# <Task title> — Codex report

## Changes actually made
## Verification actually run
## Acceptance criteria
## Limitations
## Remaining blockers
## Explicit non-goals
## Git state
```

Verdicts:

- `PASS`: every acceptance criterion is satisfied.
- `PASS_WITH_LIMITATIONS`: goal satisfied with material non-blocking limitations.
- `BLOCKED`: completion requires a genuine human decision or unavailable external prerequisite.
- `FAIL`: acceptance criteria remain unsatisfied and machine-solvable work remains.

For repository-changing tasks, report initial/final branch, HEAD, upstream, worktree state, and whether final `HEAD == upstream` was safely achieved.
