# Codex report template

Codex reports live at:

```text
reports/codex/YYMMDD_codex_NN.md
```

A report records execution evidence; it does not redefine project design or operational policy. Its `verdict` is Codex's execution-status claim and is evidence for ChatGPT's independent acceptance review, not final acceptance by itself.

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
### Layer 1 — Component / property
### Layer 2 — Contract / invariant
### Layer 3 — Integration
### Layer 4 — Real-artifact regression
### Layer 5 — E2E / recovery / repeatability
### Layer 6 — Release / non-functional
## Acceptance criteria
## Limitations
## Remaining blockers
## Explicit non-goals
## Git state
```

Under `## Verification actually run`, report each evidence layer required by the task's verification plan.

For every required layer, record concrete evidence such as commands, test counts, artifacts, environments, run IDs, hashes, or observed failure/recovery behavior as appropriate. If a planned check was skipped, unavailable, or materially changed, state that explicitly rather than silently omitting it.

Layers marked `N/A` by the task do not need fabricated evidence; retain them only when useful for making the report's scope unambiguous.

Do not treat a single `pytest PASS`, coverage percentage, scanner result, or CI badge as a substitute for a different required evidence layer. The report should make clear which acceptance claim each result supports.

Techniques such as property/fuzz testing, branch coverage, mutation testing, fault injection, concurrency/race testing, and benchmarking should be reported inside the relevant evidence layer rather than as additional pseudo-levels.

Execution-verdict meanings:

- `PASS`: Codex found every task acceptance criterion and every required verification layer satisfied by the reported evidence.
- `PASS_WITH_LIMITATIONS`: Codex found the goal satisfied with material non-blocking limitations; the affected evidence layer(s) must be named.
- `BLOCKED`: completion requires a genuine human decision or unavailable external prerequisite.
- `FAIL`: acceptance criteria or required evidence remain unsatisfied and machine-solvable work remains.

ChatGPT independently reviews the report and underlying evidence, including whether the selected verification level and evidence-layer plan were appropriate. The User retains final decision/override authority.

For repository-changing tasks, report initial/final branch, HEAD, upstream, worktree state, and whether final `HEAD == upstream` was safely achieved.
