# ChatGPT FORMAL task template

Cold path: load this file only when creating or reviewing a FORMAL task artifact.

FORMAL lifecycle/acceptance/integration is owned by `../formal.md`; report filename/common metadata/archive rules by `../../project/reports.md`; local Git/worktree/tmp mechanics by `../execution.md`; verification evidence design by `../verification.md`.

FORMAL tasks live at:

```text
reports/chatgpt/YYMMDD_chatgpt_NN.md
```

The committed task is the sole task-specific execution specification. Detailed task content MUST NOT be repeated in chat.

## Before issuing

ChatGPT must have:

```text
refreshed current collaboration authority
→ inspected current project authority/evidence
→ completed design-bearing decisions before task issue
→ for Skill behavior changes: updated current design + SKILL.md/references first
→ partitioned ChatGPT-authorable work from genuinely local work
→ completed DIRECT code/tests/checks it can correctly perform
→ resolved activated shared coding-Skill authorities
→ selected verification level + remaining evidence
→ selected dedicated task branch unless explicitly excepted
→ pinned exact collaboration revision
```

Keep one FORMAL task to one reviewable logical responsibility.

## Required metadata

```yaml
---
artifact_type: chatgpt_task
artifact_id: <YYMMDD_chatgpt_NN>
task_id: <TASK_ID>
title: <SHORT_TITLE>
date: <YYYY-MM-DD>
project: <PROJECT_NAME>
repository: <OWNER/REPOSITORY>
status: issued
execution_mode: formal
summary: >
  <PURPOSE/SCOPE>
task_branch: <TASK_BRANCH>
baseline_sha: <DIRECT_TASK_BASELINE_SHA>
verification_level: <level_1 | level_2 | level_3>
collaboration_commit: <PINNED_AGENT_COLLABORATION_SHA>
coding_skill_profile: >
  cigit-zgy/agent-collaboration@<PINNED_AGENT_COLLABORATION_SHA>:
  references/collaboration/shared-coding-skills.md
codex_report: reports/codex/<YYMMDD_codex_NN.md>
---
```

`artifact_id` equals the filename stem. `baseline_sha` is the exact authorized repository baseline prepared by ChatGPT before the task artifact. `codex_report` is the exact expected report path.

## Body

Use the smallest task body that fully specifies execution. Typical sections are:

```markdown
# <Task title>

## Mission
## Authority and frozen semantics
## Shared coding Skills and authoring state
## LOCAL scope
## Required changes
## Non-goals / ownership boundary
## Engineering constraints
## Acceptance criteria
## Verification
## Git / synchronization / integration
## Codex report
```

Bind exact current `design/` + committed `SKILL.md`/reference owners for Skill behavior changes. List only verification categories actually required.

## Remote synchronization — hard requirement

Every repository-changing FORMAL task inherits the two-sided remote synchronization handshake in `../execution.md` and MUST NOT weaken it.

Before any mutation Codex must:

```text
fresh-fetch remote refs
→ resolve exact task branch + committed task coordinate + authorized baseline
→ inspect local branch/HEAD/upstream/worktrees/User state
→ establish the task worktree safely
→ prove local execution HEAD == authorized fetched remote baseline
```

If the fetched remote task branch/task coordinate is not the expected issued state, Codex stops rather than silently working from a stale or unexpected baseline.

After task changes Codex must:

```text
commit task-scoped changes
→ push task branch
→ fresh-fetch remote refs again
→ prove local task HEAD == fetched upstream task-branch HEAD
→ record that evidence in the Codex report
```

A successful push command alone is not sufficient. If final local/upstream equality is not established, the FORMAL task cannot report PASS.

Do not use blind `git pull`, destructive reset, rebase, stash, force checkout, or force push merely to synchronize.

## Skill behavior tasks — hard requirement

```text
User + ChatGPT adjudication
→ current design updated
→ SKILL.md + references updated
→ committed task points to those exact owners
→ Codex implements/repairs code to conform
→ tests probe the general Skill contract
```

Codex MUST NOT create task-specific production semantics when durable Skill design is missing or ambiguous. If local execution discovers a new design gap, report `DESIGN_GAP` and stop the affected path.

## ChatGPT-first authoring

ChatGPT completes code/tests it can correctly author before handoff. Local verification need alone does not transfer all implementation authorship to Codex.

## User-visible launch locator — hard requirement

After commit/push, ChatGPT may provide at most one short informational sentence before the locator. It MUST NOT paste or summarize the detailed task.

Emit exactly one fenced `text` block:

```text
执行 FORMAL 任务：
Repository: <LOCAL_REPOSITORY_OR_OWNER/REPO>
Task: reports/chatgpt/<TASK_FILE>.md
Task commit: <TASK_COMMIT>
任务链接如下：
https://github.com/<OWNER>/<REPOSITORY>/blob/<TASK_COMMIT>/reports/chatgpt/<TASK_FILE>.md
以 committed task 为唯一 task-specific 执行规范。
```

Do not include task steps, command lists, prohibitions, acceptance criteria, branch mechanics, verification detail, collaboration pin, or design explanation in the chat locator; those belong in the committed task.

Do not append task-specific prose after the block.

If the task cannot be committed/pushed, do not fabricate a remote link and do not substitute a long chat-only task. State the repository-write blocker.
