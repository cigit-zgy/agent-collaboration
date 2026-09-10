# Exceptional conversation-handoff template

Cold path: load this file only when `../handoff.md` has determined that real conversation-only delta exists.

Normal conversation resume uses `../current.md` and does not need this template.

## Size target

A handoff is a tiny residual-delta artifact:

```text
normal target <= 4 KiB
review above ~8 KiB
```

If the content is largely recoverable from AGENTS, CURRENT, design, task/report, concept, Git history, or another repository owner, do not create the handoff.

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
  <one compact sentence describing the residual conversation-only delta>
repository_head: <SHA_AT_HANDOFF_CREATION>
collaboration_authority: cigit-zgy/agent-collaboration@<SHA>
previous_handoff: <OPTIONAL_PROVENANCE_ONLY>
---
```

Omit `previous_handoff` when it adds no provenance value. It never creates a required reading chain.

Handoffs live only at:

```text
reports/handoff/YYMMDD_handoff_NN.md
```

## Minimal body

Use only what actually exists:

```markdown
# Conversation-only delta

## Residual context
- <few facts that cannot safely live in another current owner>

## Unresolved edge
- <only if the residual delta affects an unresolved decision>

## Resume pointer
- Current state: `CURRENT.md`
- <one directly relevant owner if needed>
```

Do not add empty sections.

## Authoring check

Before each sentence ask:

```text
Can the next conversation recover this cheaply from a current repository owner?
```

If yes, delete the sentence and keep at most a pointer when necessary.

Never reproduce:

```text
full project overview
current design text
CURRENT.md content
task/report bodies
test summaries
old decision history
commit history
previous handoffs
conversation transcript
```

## New-conversation start instruction

Keep the User-facing resume prompt short, for example:

```text
Continue <OWNER/REPOSITORY>.
This is conversation resume, not project migration.
Recover from AGENTS.md → CURRENT.md → design/README.md.
CURRENT points to reports/handoff/<THIS_FILE> for one exceptional residual delta; read only that handoff and then continue just in time.
```

Do not paste the handoff body into the chat prompt.

## Quality check

A good handoff contains information that would genuinely be lost if the old conversation disappeared. If the handoff can be deleted without losing such information, it should not have been created.
