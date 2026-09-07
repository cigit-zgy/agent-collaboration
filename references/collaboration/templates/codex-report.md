# Codex report template

Formal Codex reports live only at:

```text
reports/codex/YYMMDD_codex_NN.md
```

FORMAL lifecycle is owned by `../formal.md`; report filename/common metadata/archive rules by `../../project/reports.md`; remote synchronization/Git safety by `../execution.md`.

A report records implementation/execution evidence. It does not redefine project design or collaboration policy, and its verdict is not final acceptance.

## Required metadata

```yaml
---
artifact_type: codex_report
artifact_id: <YYMMDD_codex_NN>
task_id: <TASK_ID>
title: <SHORT_TITLE>
date: <YYYY-MM-DD>
project: <PROJECT_NAME>
repository: <OWNER/REPOSITORY>
status: completed
summary: >
  <IMPLEMENTATION/RESULT SUMMARY>
verdict: <PASS | PASS_WITH_LIMITATIONS | BLOCKED | FAIL>
task_branch: <TASK_BRANCH>
task_source_sha: <TASK_SOURCE_SHA>
baseline_sha: <BASELINE_SHA>
final_task_head: <FINAL_LOCAL_TASK_HEAD>
upstream_task_head: <FETCHED_UPSTREAM_TASK_HEAD>
task_head_equals_upstream: <true | false>
verification_level: <level_1 | level_2 | level_3>
limitations: []
---
```

`artifact_id` equals the filename stem. For repository-changing FORMAL work, `final_task_head`, `upstream_task_head`, and `task_head_equals_upstream` are mandatory and come from the post-push fresh-fetch verification, not from assumptions about push success.

## Body

Use a concise structure:

```markdown
# <Task title> — Codex report

## Changes
## AI-assisted implementation transparency
## Shared coding-Skill alignment
## Verification evidence
## Local temporary state
## Acceptance criteria / blockers
## Git synchronization result
```

State what actually changed, including implementation already authored by ChatGPT before handoff versus implementation added/repaired by Codex. For material AI-assisted implementation, make key observable engineering choices, invariants, dependencies and limitations recoverable without exposing private chain-of-thought.

Verification evidence must map to the task's actual required categories. Do not treat a single `pytest PASS`, coverage percentage, scanner result or CI badge as a substitute for distinct required evidence.

For LOCAL work, record the task scratch boundary and final disposition. Do not claim cleanup when dirty, unpushed, active or uncertain state was deleted blindly.

Execution-verdict meanings:

```text
PASS                  every in-scope criterion/evidence claim satisfied
PASS_WITH_LIMITATIONS goal satisfied with named non-blocking limitations
BLOCKED               unavailable prerequisite or genuine higher-authority decision required
FAIL                  machine-solvable in-scope criteria remain unsatisfied
```

ChatGPT performs the acceptance review. The User retains final decision/override authority and designated human checkpoints.

## Git synchronization result — hard requirement

For repository-changing FORMAL tasks, report both sides of the synchronization handshake:

```text
PRE
fresh fetched remote task/baseline coordinate
local execution HEAD before mutation
equality / mismatch result

POST
final local task HEAD
fetched upstream task-branch HEAD after push + fresh fetch
TASK_HEAD_EQUALS_UPSTREAM = YES | NO
worktree cleanliness when required
preservation of pre-existing User state
```

A repository-changing report with `task_head_equals_upstream: false` MUST NOT use `PASS`.

Do not claim default-branch integration unless it actually occurred after acceptance.

## User-visible completion response — hard requirement

After the report-containing commit has been pushed, Codex provides the compact result locator required by the active collaboration task/report contract. The durable Markdown report remains the evidence authority.

Formal locator:

```text
VERDICT: <PASS | PASS_WITH_LIMITATIONS | BLOCKED | FAIL>
REPORT: reports/codex/<REPORT_FILE>.md
REPORT_COMMIT: <REPORT_CONTAINING_COMMIT>

报告链接如下：
https://github.com/<OWNER>/<REPOSITORY>/blob/<REPORT_CONTAINING_COMMIT>/reports/codex/<REPORT_FILE>.md
```

Use the commit that actually contains the report. If the report cannot be pushed and fresh-fetched/verifiably published, do not fabricate a remote link or claim PASS; state the publication blocker truthfully.
