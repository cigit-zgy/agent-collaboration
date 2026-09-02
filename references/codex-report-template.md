# Codex report template

Codex reports live under stable paths:

```text
reports/codex/YYMMDD_codex_NN.md
```

A report records execution evidence; it does not redefine project concepts or current
operational policy.

## YAML metadata

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
  <ONE-TO-THREE-SENTENCE IMPLEMENTATION/RESULT SUMMARY>
tags:
  - <TAG>
concepts: []
limitations: []
---
```

Rules:

- `task_source_sha` binds the report to the exact committed task Codex executed;
- do not repeat identity metadata in the body;
- do not record the commit containing the report inside that same report;
- do not move or rewrite the report later for calendar organization;
- `limitations` contains only material non-blocking limitations.

## Body template

```markdown
# <Task title> — Codex report

## Changes actually made

## Verification actually run

## Acceptance criteria

## Limitations

## Remaining blockers

## Explicit non-goals

## Git state

- Initial: <branch / HEAD / upstream / worktree summary>
- Final: <branch / HEAD / upstream / worktree summary>
- HEAD == upstream: <PASS | FAIL>
```

## Verdict meanings

- `PASS`: every acceptance criterion is satisfied.
- `PASS_WITH_LIMITATIONS`: task goal satisfied with real non-blocking limitations.
- `BLOCKED`: completion requires a genuine human decision or unavailable external
  prerequisite.
- `FAIL`: acceptance criteria are not satisfied and machine-solvable work remains.

If Codex can still fix an in-scope issue, it should continue or report `FAIL`, not
`BLOCKED`. Passing tests alone does not establish task acceptance.

For repository-changing tasks, final `HEAD == upstream` is the normal synchronization
condition when it can be achieved safely. Pre-existing User changes must remain
preserved and explicitly reported.
