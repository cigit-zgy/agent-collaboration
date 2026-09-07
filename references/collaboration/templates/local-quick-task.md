# ChatGPT LOCAL-QUICK task template

Cold path: load this file only when creating or reviewing a LOCAL-QUICK Codex task artifact.

LOCAL execution/Git/tmp rules are owned by `../execution.md`; report-family naming/metadata by `../../project/reports.md`; verification evidence design by `../verification.md` when needed.

Every LOCAL-QUICK Codex repository task is committed at:

```text
reports/chatgpt/YYMMDD_chatgpt_NN.md
```

The committed task file is the sole task-specific execution specification. Do not place the detailed task in chat.

## Required metadata

```yaml
---
artifact_type: chatgpt_task
artifact_id: <YYMMDD_chatgpt_NN>
task_id: <SHORT_TASK_ID>
title: <SHORT_TITLE>
date: <YYYY-MM-DD>
project: <PROJECT_NAME>
repository: <OWNER/REPOSITORY>
status: issued
execution_mode: local_quick
summary: >
  <ONE-SENTENCE PURPOSE>
collaboration_commit: <PINNED_AGENT_COLLABORATION_SHA>
---
```

Add task branch, baseline SHA, local root, shared coding-Skill coordinates, or other metadata only when the actual task needs them. Do not copy FORMAL-only fields merely for symmetry.

## Body

Use the smallest body that makes execution deterministic. Common sections are:

```markdown
# <Task title>

## Mission
## Authority / source coordinates
## Local scope
## Required changes
## Hard boundaries
## Verification
## Git / push
## Result contract
```

Sections are optional when unnecessary. Detailed commands, byte-integrity rules, path constraints, branch rules, stop boundaries, and exact final-output fields belong here rather than in chat.

## Mode boundary

LOCAL-QUICK is appropriate only while the task remains bounded, low-risk, and free of unresolved scientific/product/design decisions or other FORMAL triggers.

If execution discovers material scope growth, destructive/shared-state risk, unresolved design, public/trust contract change, release qualification, or another FORMAL boundary:

```text
STOP affected execution
→ return BLOCKED with the concrete escalation reason
→ do not expand the task through chat patches
→ ChatGPT issues a new FORMAL task if continuation is approved
```

## No Codex report

LOCAL-QUICK does not create `reports/codex/`.

Execution evidence is returned only through the task's compact `Result contract`, plus repository branch/commit coordinates when applicable. Do not create a formal report merely because the local command sequence is long.

## User-visible launch locator — hard UI requirement

After the task artifact is committed and pushed, ChatGPT MUST NOT paste or paraphrase the detailed task into the conversation.

At most one short sentence may precede the locator. Then emit exactly one fenced `text` block:

```text
执行 LOCAL-QUICK 任务：
Repository: <LOCAL_REPOSITORY_OR_OWNER/REPO>
Task: reports/chatgpt/<TASK_FILE>.md
Task commit: <TASK_COMMIT>
任务链接如下：
https://github.com/<OWNER>/<REPOSITORY>/blob/<TASK_COMMIT>/reports/chatgpt/<TASK_FILE>.md
以 committed task 为唯一 task-specific 执行规范；完成后只按 task 的 Result contract 返回结果。
```

Do not include task steps, command lists, prohibitions, acceptance criteria, file inventories, test matrices, or explanations after the block.

If the task cannot be committed/pushed, do not hand off a chat-only substitute. State the repository-write blocker instead.

## Result contract

The task itself defines the shortest sufficient final result, for example:

```text
VERDICT: PASS | BLOCKED | FAIL
TASK_BRANCH: <branch>
TASK_HEAD: <sha>
<task-specific critical evidence fields only>
```

Codex returns exactly that compact result unless a blocker requires one concise explanatory line. It does not repeat the task body.
