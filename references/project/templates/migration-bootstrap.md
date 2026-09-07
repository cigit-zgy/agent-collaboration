# Project migration bootstrap template

Cold path: load this file only when an old conversation needs to hand a project-policy migration to a new ChatGPT conversation.

Migration semantics are owned by `../migration.md`.

## Goal

The bootstrap is deliberately short. It carries only durable coordinates and session delta that are expensive to recover from the repository.

Do not paste collaboration rules, full project history, full concept summaries, or long Codex reports into the bootstrap.

## Required output shape

Emit exactly one fenced `text` block so the User can copy it directly:

````text
```text
请接管并将以下项目迁移到当前最新的 cigit-zgy/agent-collaboration 规范。

Repository: <OWNER/REPOSITORY>
Local repository: <LOCAL_PATH | UNKNOWN>
Project objective: <ONE OR TWO SHORT LINES>

Migration objective:
- 解析当前最新 agent-collaboration，并按 SKILL.md → references/project/migration.md 执行迁移。
- 将当前项目迁移到新的 authority/routing/report/living-design 模型；保留项目自己的科学与产品语义。
- 若 design/ 缺失或陈旧，根据当前仍有效的项目证据归约出唯一 current living design；reports/concept/ 仅作为设计历史/证据。

Current project anchors:
- AGENTS.md: <PATH>
- workflow Skill: <PATH | NONE>
- design/: <PRESENT | ABSENT | KNOWN_STALE>
- important legacy design/source pointers: <PATHS | NONE>
- newest relevant handoff: <PATH | NONE>

Active work anchor:
- branch / commit: <BRANCH + SHA | NONE>
- ChatGPT task: <PATH | NONE>
- Codex report: <PATH | NONE>
- state: <ACTIVE | BLOCKED | COMPLETED | NONE>
- unresolved blocker/design question: <1–3 SHORT BULLETS | NONE>

Session-only accepted delta not yet durable:
- <NONE OR AT MOST A FEW SHORT BULLETS>

Migration rules:
1. 先检查目标仓库当前 branch/HEAD/AGENTS 和 repository state；不要把本提示词或旧 handoff 当成当前 truth。
2. 不要预读全部 reports/concept、旧 ChatGPT/Codex reports、旧 handoffs 或整个 collaboration reference tree。
3. 只迁移真正 drift 的 surfaces；已经符合当前规范的内容不要为了统一格式重写。
4. 先完成 migration assessment，再执行 ChatGPT 能直接完成的 repository migration。
5. active task/report/blocker 必须在迁移后重新对照 current design/ 和 repository state 判断，不要直接沿用旧结论。
6. 遇到 genuine OPEN_DESIGN 时停止受影响的实现路径，交给 User + ChatGPT 裁决。
7. <DO NOT CREATE CODEX TASK YET | CODEX MAY BE USED ONLY IF LOCAL EVIDENCE IS GENUINELY REQUIRED>

第一轮先输出不超过约 1200 字的 migration assessment，明确：当前 authority、design/ 状态、需要迁移的 surfaces、active task/blocker 的真实状态，以及哪些内容明确不需要读取/修改。
```
````

## Old-conversation preparation

Before emitting the block:

```text
1. make material accepted session-only decisions durable when connected capability allows;
2. resolve the exact repository + current active task/report/branch anchors;
3. summarize the unresolved state in no more than a few bullets;
4. omit facts that the new conversation can cheaply recover from the repository;
5. use NONE rather than inventing missing coordinates.
```

## Field discipline

`important legacy design/source pointers` means only the few files the old conversation knows are unusually important for reconstructing current design. It is not a list of all concept files.

`Session-only accepted delta` should normally be `NONE`. If material accepted design is still only in chat and repository write capability is available, make it durable before migration instead of copying it into the prompt.

`unresolved blocker/design question` summarizes only the current decision edge. Do not paste the Codex report body; point to the report and state the blocker in one to three bullets.

## Quality check

A conforming bootstrap should let a new conversation start the migration without first reconstructing the old conversation, while remaining short enough that repository-native context—not pasted prose—dominates the working context.
