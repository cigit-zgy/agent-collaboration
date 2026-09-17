# Project migration bootstrap template

Cold path: load only for actual project-policy migration. Normal conversation replacement uses `../current.md`.

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
- 保留项目科学/产品语义，只修真正 drift 的 authority/routing/CURRENT/reports/design/Skill/execution surfaces。
- 若仍使用根目录 design/，先按真实责任分类/合并/去重，再建立唯一 reports/design/；不要机械搬移发散结构。
- 历史 ChatGPT/Codex/Concept/Handoff 记录保持 append-only；不要把执行历史塞进 current Design。

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

Rules:
1. 先检查当前 branch/HEAD/AGENTS/CURRENT/repository state；本提示词不是 current truth。
2. 不预读全部 concept、旧 task/report、旧 handoff、整个 reports/design tree 或整个 collaboration references。
3. 已符合规范的内容不为统一格式重写。
4. 长期/多对话框项目迁移后建立或修正唯一 root CURRENT.md。
5. 初始化/校正 reports/design/README.md 的 Design reconciliation cursor when living Design is used。
6. 每个 Codex repository task 应有 committed ChatGPT task + durable Codex record。
7. genuine OPEN_DESIGN 交给 User + ChatGPT 裁决。
8. <DO NOT CREATE CODEX TASK YET | CODEX MAY BE USED ONLY IF LOCAL EVIDENCE IS GENUINELY REQUIRED>

第一轮只给 compact migration assessment；不要先做项目历史总结。
```
````

Do not use this template merely because an old conversation is full.

Normal resume is:

```text
继续 <OWNER/REPOSITORY>。
按 AGENTS.md → CURRENT.md 恢复当前工作；
若 CURRENT 指向 handoff，只读取那个 handoff，然后按需读取一个 current owner。
不要预读其他历史。
```
