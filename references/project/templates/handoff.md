# Conversation-handoff template

Load only when the User explicitly ends/replaces a long conversation under `../handoff.md`.

Target `<= 2 KiB`.

Handoffs live at `reports/handoff/YYMMDD_handoff_NN.md` and are append-only.

## Metadata

```yaml
---
artifact_type: conversation_handoff
artifact_id: <YYMMDD_handoff_NN>
record_kind: conversation_boundary
title: <SHORT_TITLE>
date: <YYYY-MM-DD>
project: <PROJECT_NAME>
repository: <OWNER/REPOSITORY>
status: current_snapshot
summary: >
  <one sentence>
period_start: <YYYY-MM-DD or report coordinate>
period_end: <YYYY-MM-DD or report coordinate>
chatgpt_reports: []
codex_reports: []
concept_reports: []
repository_head: <SHA_AT_HANDOFF_CREATION>
collaboration_authority: cigit-zgy/agent-collaboration@<SHA>
design_signal: none
---
```

Use report ranges/paths rather than copying report bodies.

## Minimal body

```markdown
# Conversation handoff

## Current work edge
<one compact paragraph or bullets>

## Active coordinates
- <branch/task/report only when needed>

## Unresolved edges
- <0–3 items>

## Next action
<exactly one action>
```

Do not reproduce project overview, Design text, scientific background, test summaries, task/report bodies, old decisions, commit history, previous handoffs, or transcript text.

## New-conversation prompt

```text
继续 cigit-zgy/<repository>。

按 AGENTS.md → CURRENT.md 恢复当前工作；
仅读取 CURRENT.md 指向的 handoff：reports/handoff/<THIS_FILE>。
不要预读其他历史。
```

Do not paste the handoff body into the prompt.
