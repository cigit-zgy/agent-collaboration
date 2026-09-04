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

## Shared coding-Skill alignment

## Verification evidence

## Acceptance criteria / blockers

## Git result
```

## Changes

State what was actually changed, including material files/modules/artifacts. Do not restate the full task specification.

Distinguish:

```text
implementation/tests already authored by ChatGPT before handoff
implementation added or repaired by Codex after local execution
```

## AI-assisted implementation transparency

For material implementation work, make these items recoverable when applicable:

```text
implementation generated/modified by ChatGPT, Codex, or other AI tooling
key implementation choice and why it was selected
main data/control flow affected
important invariants/failure boundaries
new or removed dependency/abstraction and why
known limitations/deviations/non-goals
```

Keep this section concise. It exists so the implementation can be audited without requiring the User to read every line of code or reconstruct the generation conversation.

Do not expose private chain-of-thought. Report design-relevant rationale and observable engineering decisions only.

## Shared coding-Skill alignment

When the task activates cross-Agent coding Skills, record:

```text
shared profile coordinate
activated Skill names/modes
immutable authority coordinates
local discovered/cache revision
MATCH | ALIGNED_TO_PIN | REMOTE_PIN_USED | BLOCKED
any safe alignment action actually performed
```

Check only Skills activated by the task. Do not report or update the complete machine Skill inventory merely for ceremony.

A local Skill name/path without a verified source revision is not alignment evidence. If Codex used a local-only helper, state that it did not override the shared coding contract.

## Verification evidence

Report each remaining evidence category required by the task using concrete evidence such as commands, test counts, artifacts, environments, run IDs, hashes, or observed failure/recovery behavior.

Separate checks already completed by ChatGPT from checks run locally by Codex. Rerun a prior check only when it is needed against the final branch state or proves a distinct local-environment claim.

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

## User-visible completion response — hard requirement

After the report-containing commit has been pushed, Codex's final console response has two layers:

```text
1. concise human-readable result synopsis
2. boxed formal result locator
```

The durable Markdown report remains the full execution/evidence authority. The console synopsis is informational only and MUST NOT become a second report.

## Result synopsis — hard requirement

Codex MUST provide approximately ten short lines summarizing the result before the boxed locator.

Normal conformance target:

```text
8–12 short lines
```

Each line should communicate at most one high-level fact. The synopsis should normally cover the most useful items, for example:

```text
verdict
overall implementation/local-verification result
what ChatGPT had authored before handoff
what Codex repaired or added
shared coding-Skill alignment result
most important verification result
real-artifact/E2E result when material
material limitation or blocker
Git/task-branch state
readiness/integration implication
```

The synopsis MUST remain substantially shorter than the report. It MUST NOT dump command output, full test matrices, recovery counters, validator-message cases, acceptance tables, hashes for every artifact, or detailed implementation chronology.

Every statement in the synopsis must be supported by the durable report. If the synopsis and report differ, the report is authoritative evidence.

## Formal result locator — boxed exact format

After the synopsis, Codex MUST place the formal result locator in one fenced plain-text code block:

```text
VERDICT: <PASS | PASS_WITH_LIMITATIONS | BLOCKED | FAIL>
REPORT: reports/codex/<REPORT_FILE>.md
REPORT_COMMIT: <REPORT_CONTAINING_COMMIT>

报告链接如下：
https://github.com/<OWNER>/<REPOSITORY>/blob/<REPORT_CONTAINING_COMMIT>/reports/codex/<REPORT_FILE>.md
```

Use the commit that actually contains the report. A repository-relative path, local filesystem path, commit SHA alone, or prose reference is not a substitute for the full HTTPS link.

The report Markdown does not self-record this commit-pinned URL because the report cannot contain the SHA of the commit that contains itself. The post-commit console output is the authoritative place for this immutable report link.

FORMAL tasks MUST NOT define a custom verbose final-stdout schema that expands this box into a second report. Detailed test-by-test PASS/FAIL, implementation SHAs, recovery counters, validator states, acceptance matrices, or detailed blockers belong in the durable report and may be summarized only at high level in the 8–12-line synopsis.

If the report cannot be pushed and no truthful directly openable GitHub URL exists, do not fabricate one. Provide the 8–12-line synopsis with the publication blocker, then use this boxed form:

```text
VERDICT: <BLOCKED | FAIL>
REPORT: <LOCAL_OR_REPOSITORY_RELATIVE_REPORT_PATH>
REPORT_COMMIT: UNAVAILABLE

报告链接如下：
UNAVAILABLE — <concrete publication/push blocker>
```

An unpublished report must never be represented as remotely inspectable.

A FORMAL completion response is non-conforming when any of these occurs:

- no 8–12-line concise synopsis is provided without a concrete reason;
- the boxed locator is replaced by a long custom stdout/evidence dump;
- activated shared coding-Skill alignment is omitted from the durable report;
- the report conflates ChatGPT-authored implementation with Codex-local repair/verification.
