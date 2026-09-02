# Codex report template

Codex implementation reports live under `reports/codex/` and use:

```text
YYMMDD_codex_NN.md
```

Every report begins with compact YAML front matter for retrieval and indexing. Keep it factual and concise. Do not attempt to record the commit that contains the report inside that same report; Git history and final stdout own that value.

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
  <ONE-TO-THREE-SENTENCE IMPLEMENTATION AND RESULT SUMMARY>
tags:
  - <TAG>
concepts:
  - <CONCEPT_ID_OR_FILE>
limitations:
  - <SHORT_LIMITATION>
---
```

Metadata rules:

- `summary` states what was actually implemented and the resulting state; do not copy the Changes section verbatim.
- `tags` contains only a few stable retrieval terms.
- `concepts` lists durable concept assets materially relevant to the implementation; use `[]` when none.
- `limitations` contains only material non-blocking limitations; use `[]` when none.
- `verdict` uses an underscore in YAML (`PASS_WITH_LIMITATIONS`) while the human-readable body keeps `PASS WITH LIMITATIONS`.
- do not add speculative metadata fields or self-referential final commit SHAs.

```markdown
# <Task title> — Codex Report

VERDICT: <PASS | PASS WITH LIMITATIONS | BLOCKED | FAIL>
Task ID: <TASK_ID>
Task source SHA: <TASK_SOURCE_SHA>
Baseline SHA: <BASELINE_SHA>
Final SHA: <FINAL_SHA_IF_KNOWN_WITHOUT_SELF_REFERENCE>
Verification level: <LEVEL>

## Changes actually made

## Verification actually run

## Acceptance criteria

## Limitations

## Remaining blockers

## Explicit non-goals

## Git state

Initial branch: <BRANCH>
Initial HEAD: <SHA>
Initial upstream: <REF + SHA>
Initial worktree: <CLEAN | PRESERVED USER CHANGES + SUMMARY>
Final branch: <BRANCH>
Final HEAD: <SHA>
Final upstream: <REF + SHA>
Final worktree: <CLEAN | PRESERVED USER CHANGES + SUMMARY>
HEAD == upstream: <PASS | FAIL>
```

## Verdict meanings

- `PASS`: every acceptance criterion is satisfied.
- `PASS WITH LIMITATIONS`: the task goal is satisfied, with real, non-blocking, explicitly recorded limitations.
- `BLOCKED`: the unresolved issue cannot reasonably be solved by the current Agent because it requires a human decision, an unavailable external system, or genuinely insufficient source evidence.
- `FAIL`: acceptance criteria are not satisfied and machine-solvable work remains.

If Codex can still fix the issue, it must continue fixing or report `FAIL`; it must not report `BLOCKED`. Never claim `PASS` without running the required verification. Do not present planned work as completed, equate a passing test with task acceptance, or hide unfinished scope.

For repository-changing tasks, `HEAD == upstream` is the normal Git completion condition. A failed or unsafe synchronization must be reported explicitly and cannot be hidden behind a task-level PASS.

A Codex report records implementation evidence; it does not redefine durable project concepts. Durable decisions belong in `reports/concept/`.
