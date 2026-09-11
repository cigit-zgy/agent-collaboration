# Project migration bootstrap template

Cold path: load this only for actual project-policy migration. Normal conversation replacement uses `../current.md`.

## Required output shape

Emit one short fenced `text` block:

````text
```text
请将以下已有项目迁移到当前最新的 cigit-zgy/agent-collaboration 规范。
这是 project-policy migration，不是普通 conversation resume。

Repository: <OWNER/REPOSITORY>
Local repository: <LOCAL_PATH | UNKNOWN>
Project objective: <ONE OR TWO SHORT LINES>

Migration objective:
- 按 SKILL.md → references/project/migration.md 执行 delta migration。
- 保留项目科学/产品语义，只迁移真正 drift 的 authority/routing/CURRENT/reports/design/Skill/execution surfaces。
- 若仍使用根目录 design/，迁移为 reports/design/，不要重写设计语义。

Current anchors:
- AGENTS.md: <PATH>
- CURRENT.md: <PRESENT | ABSENT | KNOWN_STALE>
- workflow Skill: <PATH | NONE>
- reports/design/: <PRESENT | ABSENT | KNOWN_STALE>
- legacy root design/: <PRESENT | ABSENT>

Active work:
- branch / commit: <BRANCH + SHA | NONE>
- ChatGPT task: <PATH | NONE>
- Codex report: <PATH | NONE>
- state: <ACTIVE | BLOCKED | COMPLETED | NONE>
- unresolved migration/design question: <1–3 SHORT BULLETS | NONE>

Session-only accepted delta not yet durable:
- <NONE OR AT MOST A FEW SHORT BULLETS>

Rules:
1. 先检查当前 branch/HEAD/AGENTS/CURRENT/repository state；本提示词不是 current truth。
2. 不预读全部 concept、旧 task/report、旧 handoff、整个 reports/design tree 或整个 collaboration references。
3. 已符合规范的内容不为统一格式重写。
4. 长期/多对话框项目迁移后建立或修正唯一 root CURRENT.md。
5. active task/report/blocker 重新对照 current reports/design 和 repository state 判断。
6. genuine OPEN_DESIGN 交给 User + ChatGPT 裁决。
7. <DO NOT CREATE CODEX TASK YET | CODEX MAY BE USED ONLY IF LOCAL EVIDENCE IS GENUINELY REQUIRED>

第一轮只给 compact migration assessment；不要先做项目历史总结。
```
````

Do not use this template merely because an old conversation is full.

Normal resume is:

```text
Continue <OWNER/REPOSITORY>.
This is conversation resume, not project migration.
Recover from AGENTS.md → CURRENT.md → reports/design/README.md.
Load only the current concern just in time; do not preload history.
```
