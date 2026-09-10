# Project migration bootstrap template

Cold path: load this file only when an old conversation needs to hand an actual **project-policy migration** to a new ChatGPT conversation.

Normal replacement of a full conversation uses `../current.md` and does not use this template.

Migration semantics are owned by `../migration.md`.

## Goal

The bootstrap is deliberately short. It carries repository coordinates, the actual migration objective, and only session delta that is expensive to recover from the repository.

Do not paste collaboration rules, full project history, concept summaries, or Codex reports into the bootstrap.

## Required output shape

Emit exactly one fenced `text` block:

````text
```text
请将以下已有项目迁移到当前最新的 cigit-zgy/agent-collaboration 规范。
这是 project-policy migration，不是普通 conversation resume。

Repository: <OWNER/REPOSITORY>
Local repository: <LOCAL_PATH | UNKNOWN>
Project objective: <ONE OR TWO SHORT LINES>

Migration objective:
- 按当前 agent-collaboration SKILL.md → references/project/migration.md 执行 delta migration。
- 保留项目自己的科学/产品语义，只迁移真正 drift 的 authority/routing/CURRENT/design/reports/Skill/execution surfaces。

Current anchors:
- AGENTS.md: <PATH>
- CURRENT.md: <PRESENT | ABSENT | KNOWN_STALE>
- workflow Skill: <PATH | NONE>
- design/: <PRESENT | ABSENT | KNOWN_STALE>
- important legacy design/source pointers: <PATHS | NONE>

Active work:
- branch / commit: <BRANCH + SHA | NONE>
- ChatGPT task: <PATH | NONE>
- Codex report: <PATH | NONE>
- state: <ACTIVE | BLOCKED | COMPLETED | NONE>
- unresolved migration/design question: <1–3 SHORT BULLETS | NONE>

Session-only accepted delta not yet durable:
- <NONE OR AT MOST A FEW SHORT BULLETS>

Rules:
1. 先检查目标仓库当前 branch/HEAD/AGENTS/CURRENT/repository state；不要把本提示词当 current truth。
2. 不要预读全部 reports/concept、旧 task/report、旧 handoff、整个 design tree 或整个 collaboration reference tree。
3. 只迁移真正 drift 的 surfaces；已经符合规范的内容不要为了统一格式重写。
4. 若项目是长期/多对话框项目，迁移完成后按 current.md 建立或修正唯一 root CURRENT.md。
5. active task/report/blocker 必须重新对照 current design 和 repository state 判断。
6. genuine OPEN_DESIGN 交给 User + ChatGPT 裁决。
7. <DO NOT CREATE CODEX TASK YET | CODEX MAY BE USED ONLY IF LOCAL EVIDENCE IS GENUINELY REQUIRED>

第一轮只给 compact migration assessment；不要先做项目历史总结。
```
````

## Old-conversation preparation

Before emitting the block:

```text
1. make material accepted session-only decisions durable when connected capability allows;
2. update CURRENT.md if the target project already uses it;
3. resolve exact repository + active task/report/branch anchors;
4. summarize unresolved migration state in no more than a few bullets;
5. omit facts the new conversation can cheaply recover from repository owners;
6. use NONE rather than inventing missing coordinates.
```

## Do not use for normal conversation replacement

If the repository already conforms to collaboration and the only event is that the old chat is full, do not issue this bootstrap.

Use the normal resume instruction instead:

```text
Continue <OWNER/REPOSITORY>.
This is conversation resume, not project migration.
Recover from AGENTS.md → CURRENT.md → design/README.md.
Load only the current concern just in time; do not preload history.
```

## Quality check

A conforming migration bootstrap lets a new conversation inspect and migrate repository drift without reconstructing the old conversation. A normal conversation switch should not need this artifact at all.
