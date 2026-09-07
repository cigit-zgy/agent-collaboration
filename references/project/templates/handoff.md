# Conversation handoff authoring template

Load this template only when ChatGPT is creating a new project conversation handoff. Context recovery does not need this file.

Handoff lifecycle is owned by `../handoff.md`; project-policy migration is owned by `../migration.md`; report filename/common metadata/archive rules are owned by `../reports.md`.

## Size guidance

The handoff is a pointer-first continuity artifact. Repository-native current state should remain the main source of truth.

```text
simple conversation handoff   100–180 lines
complex active project        180–300 lines
major unresolved design phase 300–400 lines
```

The normal target is **120–250 lines**. A handoff above roughly 400 lines is a signal to inspect whether current design, concept history, task/report text, logs, or transcript material has been duplicated instead of referenced.

Do not create a long handoff merely to migrate a project to a new collaboration policy. Use `migration.md` and `templates/migration-bootstrap.md` for that purpose.

## Required metadata

Use compact YAML front matter:

```yaml
---
artifact_type: conversation_handoff
artifact_id: <YYMMDD_handoff_NN>
title: <SHORT_RECOVERY_TITLE>
date: <YYYY-MM-DD>
project: <PROJECT_NAME>
repository: <OWNER/REPOSITORY>
status: current_snapshot
summary: >
  <compact searchable recovery summary>
handoff_id: <YYMMDD_handoff_NN>
source_conversation_title: <TITLE_OR_SHORT_IDENTIFIER>
source_period:
  start: <YYYY-MM-DD_OR_UNKNOWN>
  end: <YYYY-MM-DD>
repository_head: <SHA_AT_HANDOFF_CREATION>
default_branch: <BRANCH>
collaboration_authority: cigit-zgy/agent-collaboration@<SHA>
previous_handoff: <NONE_OR_reports/handoff/YYMMDD_handoff_NN.md>
source_conversation_url: <OPTIONAL_IF_TRUTHFULLY_AVAILABLE>
---
```

`artifact_id` and `handoff_id` both equal the filename stem. Omit `source_conversation_url` when no stable truthful URL is available. Do not invent conversation IDs or URLs.

Handoffs live only at:

```text
reports/handoff/YYMMDD_handoff_NN.md
```

Do not create a repository-root `handoff/` or `reports/handoff/README.md`.

## Default body

Use only sections carrying continuity that is not already cheap to recover from current repository-native owners:

```markdown
# Conversation handoff — <project / phase>

## 1. Project objective / current work edge
## 2. Current authority pointers
## 3. Current repository and active task state
## 4. Settled decisions / rejected directions that remain expensive to reconstruct
## 5. Unresolved decisions / blockers
## 6. Next actions
## 7. Source pointers / raw provenance
```

A section may be omitted when it has no useful content. Do not fill empty sections with `N/A` ceremony.

## Section guidance

Current authority pointers should normally identify:

```text
project AGENTS.md
current design/README.md + directly relevant design topic(s)
workflow Skill/reference owners
scientific source/evidence authority
active FORMAL task when any
```

`reports/concept/` is design history, not current design authority. Include concept-note pointers only when a specific rationale remains relevant.

Do not copy current design text into the handoff. Do not reproduce a Codex report body; link it and summarize only the active consequence.

The current work edge should make clear what is actually unresolved now, not narrate every completed task.

## Authoring procedure

```text
1. resolve current project/collaboration authority;
2. make material accepted session-only state durable in repository-native owners when possible;
3. inspect current repository state + directly relevant active task/report/design artifacts;
4. resolve the newest existing handoff only for previous_handoff/continuity needs;
5. summarize only non-redundant continuity from the source conversation;
6. create reports/handoff/YYMMDD_handoff_NN.md;
7. commit/push;
8. give the User the committed path/link and a minimal new-conversation start instruction when useful.
```

## Quality check

A fresh Agent should be able to resume the current work edge from this handoff plus current repository-native authority without reading several older handoffs or reconstructing the prior conversation.
