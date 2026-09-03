# Codex report template

Formal Codex reports live at:

```text
reports/codex/YYMMDD_codex_NN.md
```

A report records implementation/execution evidence. It does not redefine project design or collaboration policy, and its verdict is not final acceptance.

## Metadata

```yaml
---
artifact_type: codex_report
task_id: <TASK_ID>
title: <SHORT_TITLE>
verdict: <PASS | PASS_WITH_LIMITATIONS | BLOCKED | FAIL>
date: <YYYY-MM-DD>
repository: <OWNER/REPOSITORY>
task_branch: <TASK_BRANCH>
task_source_sha: <TASK_SOURCE_SHA>
baseline_sha: <BASELINE_SHA>
verification_level: <level_1 | level_2 | level_3>
summary: >
  <IMPLEMENTATION/RESULT SUMMARY>
limitations: []
---
```

## Body

Use a concise structure:

```markdown
# <Task title> — Codex report

## Changes

## AI-assisted implementation transparency

## Verification evidence

## Acceptance criteria / blockers

## Git result
```

## Changes

State what was actually changed, including material files/modules/artifacts. Do not restate the full task specification.

## AI-assisted implementation transparency

For material implementation work, make these items recoverable when applicable:

```text
implementation generated/modified by Codex or other AI tooling
key implementation choice and why it was selected
main data/control flow affected
important invariants/failure boundaries
new or removed dependency/abstraction and why
known limitations/deviations/non-goals
```

Keep this section concise. It exists so the implementation can be audited without requiring the User to read every line of code or reconstruct the generation conversation.

Do not expose private chain-of-thought. Report design-relevant rationale and observable engineering decisions only.

## Verification evidence

Report each evidence category required by the task using concrete evidence such as commands, test counts, artifacts, environments, run IDs, hashes, or observed failure/recovery behavior.

Only required categories need headings. For example:

```markdown
### Contract / invariant
...

### Real artifact / external tool
...

### E2E / recovery / repeatability
...
```

If a planned check was skipped, unavailable, or materially changed, state that explicitly.

Do not treat a single `pytest PASS`, coverage percentage, scanner result, or CI badge as a substitute for another required evidence category.

Strengthening techniques such as fuzzing, mutation testing, fault injection, concurrency testing, or benchmarking are reported under the evidence category whose risk they address.

## Acceptance criteria / blockers

Map the reported evidence to the task's acceptance criteria. State remaining blockers or material limitations directly.

Execution-verdict meanings:

- `PASS`: every in-scope acceptance criterion and required evidence claim is satisfied;
- `PASS_WITH_LIMITATIONS`: the goal is satisfied with material non-blocking limitations that are explicitly named;
- `BLOCKED`: completion requires an unavailable prerequisite or genuine higher-authority decision;
- `FAIL`: in-scope acceptance criteria remain unsatisfied and machine-solvable work remains.

ChatGPT performs the acceptance review. The User retains final decision/override authority and designated human decision checkpoints.

## Git result

For repository-changing FORMAL tasks, report:

```text
initial task branch / HEAD / upstream / worktree condition
final task branch HEAD
pushed upstream HEAD
whether task-branch local HEAD == tracked upstream
pre-existing User state preserved
```

Do not claim default-branch integration unless it actually occurred after acceptance. The task report may end with a validated task branch awaiting ChatGPT acceptance/integration.

## Final console output — hard requirement

Detailed implementation, verification, acceptance evidence, hashes, test matrices, recovery behavior, and limitations belong in this report. Do not duplicate them into the terminal response.

After the report-containing commit has been pushed, Codex's normal final console response MUST use this minimal fixed format:

```text
VERDICT: <PASS | PASS_WITH_LIMITATIONS | BLOCKED | FAIL>
报告链接如下：
https://github.com/<OWNER>/<REPOSITORY>/blob/<REPORT_CONTAINING_COMMIT>/reports/codex/<REPORT_FILE>.md
```

This console block is a result locator, not a second report.

FORMAL tasks MUST NOT define a custom verbose final-stdout schema that repeats report fields such as test-by-test PASS/FAIL, implementation SHAs, recovery counters, validator states, acceptance matrices, or detailed blockers. Those facts belong in the durable report.

If immediate operator action genuinely requires one short value that cannot reasonably wait for opening the report, the task MAY add at most one concise line after the link. This exception must not become a second evidence summary.

Use the commit that actually contains the report. A repository-relative path, local filesystem path, commit SHA alone, or prose reference is not a substitute for the full HTTPS link.

The report Markdown does not self-record this commit-pinned URL because the report cannot contain the SHA of the commit that contains itself. The post-commit console output is the authoritative place for this immutable report link.

If the report cannot be pushed and no truthful directly openable GitHub URL exists, do not fabricate one. The final console response MUST instead use:

```text
VERDICT: <BLOCKED | FAIL>
报告链接如下：
UNAVAILABLE — <concrete publication/push blocker>
本地报告路径： <LOCAL_OR_REPOSITORY_RELATIVE_REPORT_PATH>
```

An unpublished report must never be represented as remotely inspectable.
