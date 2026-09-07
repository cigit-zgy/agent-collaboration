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

For a **repository-changing** LOCAL-QUICK task, also record:

```yaml
task_branch: <TASK_OR_WORK_BRANCH>
baseline_sha: <AUTHORIZED_REMOTE_BASELINE_SHA>
```

The task locator commit remains the durable task-spec coordinate. `baseline_sha` identifies the repository state from which mutation is authorized; do not infer it from a stale local checkout.

Add local root, shared coding-Skill coordinates, or other metadata only when the actual task needs them.

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
## Git / synchronization
## Result contract
```

Sections are optional when unnecessary. Detailed commands, byte-integrity rules, path constraints, branch rules, stop boundaries, and exact final-output fields belong here rather than in chat.

## Remote synchronization — hard requirement for repository-changing tasks

The task MUST inherit the two-sided synchronization handshake from `../execution.md` and may not weaken it.

Before mutation:

```text
fresh fetch
→ resolve authorized remote branch/task/baseline
→ prove local execution HEAD == authorized fetched remote baseline
```

After mutation:

```text
commit
→ push owning branch
→ fresh fetch again
→ prove local HEAD == fetched upstream HEAD
```

Do not require blind `git pull`, reset, rebase, stash, or force operations merely to synchronize.

If either equality cannot be established, the task cannot return PASS.

For repository-changing LOCAL-QUICK Result contracts, include at least:

```text
TASK_BRANCH: <branch>
TASK_HEAD: <sha>
TASK_HEAD_EQUALS_UPSTREAM: YES | NO
```

Add `REMOTE_BASELINE`, `BASELINE_MATCHED`, or another concrete synchronization field when the task's risk/structure makes it useful.

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
TASK_HEAD_EQUALS_UPSTREAM: YES | NO
<task-specific critical evidence fields only>
```

Codex returns exactly that compact result unless a blocker requires one concise explanatory line. It does not repeat the task body.
