# Codex launch template

After committing and pushing the formal task, give the User only this launch block:

```text
执行正式任务：

Repository:
<LOCAL_REPOSITORY>

Task:
reports/chatgpt/<TASK_FILE>.md

Task commit:
<TASK_COMMIT>

先 fetch 并确认当前仓库状态和 baseline。
严格执行 committed task，不依据聊天补充或扩大 scope。
完成实现、规定验证、Codex report、commit 和 push。
最后输出 task 要求的固定 stdout。
```
