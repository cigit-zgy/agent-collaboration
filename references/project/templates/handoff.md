# Exceptional conversation-handoff template

Cold path: load only when `../handoff.md` has determined that real conversation-only delta exists. Normal resume uses `../current.md`.

## Size target

```text
normal target <= 4 KiB
review above ~8 KiB
```

If content is recoverable from AGENTS, CURRENT, `reports/design/`, task/report, concept, Git history, or another owner, do not create the handoff.

## Metadata

Use the common `reports.md` envelope plus only useful handoff fields:

```yaml
---
artifact_type: conversation_handoff
artifact_id: <YYMMDD_handoff_NN>
title: <SHORT_DELTA_TITLE>
date: <YYYY-MM-DD>
project: <PROJECT_NAME>
repository: <OWNER/REPOSITORY>
status: current_snapshot
summary: >
  <one compact sentence describing residual conversation-only delta>
repository_head: <SHA_AT_HANDOFF_CREATION>
collaboration_authority: cigit-zgy/agent-collaboration@<SHA>
previous_handoff: <OPTIONAL_PROVENANCE_ONLY>
---
```

Handoffs live only at `reports/handoff/YYMMDD_handoff_NN.md`.

## Minimal body

```markdown
# Conversation-only delta

## Residual context
- <few facts that cannot safely live in another current owner>

## Unresolved edge
- <only when needed>

## Resume pointer
- Current state: `CURRENT.md`
- Current design index: `reports/design/README.md`
- <one directly relevant owner when needed>
```

Do not reproduce project overview, current design text, CURRENT content, task/report bodies, test summaries, old decision history, commit history, previous handoffs, or transcript text.

## New-conversation start instruction

```text
Continue <OWNER/REPOSITORY>.
This is conversation resume, not project migration.
Recover from AGENTS.md → CURRENT.md → reports/design/README.md.
CURRENT points to reports/handoff/<THIS_FILE> for one exceptional residual delta; read only that handoff and continue just in time.
```

Do not paste the handoff body into the chat prompt.
