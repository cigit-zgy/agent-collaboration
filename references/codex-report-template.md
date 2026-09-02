# Codex Agent report template

```markdown
# <Task title> — Agent Report

VERDICT: <PASS | PASS WITH LIMITATIONS | BLOCKED | FAIL>
Task ID: <TASK_ID>
Task source SHA: <TASK_SOURCE_SHA>
Baseline SHA: <BASELINE_SHA>
Final SHA: <FINAL_SHA>
Verification level: <LEVEL>

## Changes actually made

## Verification actually run

## Acceptance criteria

## Limitations

## Remaining blockers

## Explicit non-goals

## Git state
```

## Verdict meanings

- `PASS`: every acceptance criterion is satisfied.
- `PASS WITH LIMITATIONS`: the task goal is satisfied, with real, non-blocking,
  explicitly recorded limitations.
- `BLOCKED`: the unresolved issue cannot reasonably be solved by the current
  Agent because it requires a human decision, an unavailable external system,
  or genuinely insufficient source evidence.
- `FAIL`: acceptance criteria are not satisfied and machine-solvable work
  remains.

If Codex can still fix the issue, it must continue fixing or report `FAIL`; it
must not report `BLOCKED`. Never claim `PASS` without running the required
verification. Do not present planned work as completed, equate a passing test
with task acceptance, or hide unfinished scope.
