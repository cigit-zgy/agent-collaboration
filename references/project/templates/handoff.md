# Conversation handoff authoring template

Load this template only when ChatGPT is creating a new project conversation handoff. Context recovery does not need this file.

Handoff lifecycle is owned by `../handoff.md`; report filename/common metadata/archive rules are owned by `../reports.md`.

## Size guidance

The handoff should be information-dense enough to reconstruct the project but much shorter than the source conversation.

```text
simple migration          250–400 lines
complex project migration 400–600 lines
major architecture phase  600–800 lines
```

The usual target is 300–600 lines. A handoff above roughly 800 lines is a signal to inspect whether concept/task/report text, command logs, or transcript material has been copied unnecessarily.

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

`artifact_id` and `handoff_id` both equal the filename stem. Omit `source_conversation_url` when no stable truthful URL is available. Do not invent conversation IDs or URLs. `repository_head` anchors the repository state understood by the snapshot. `previous_handoff` supports history navigation but does not create a required reading chain.

Handoffs live only at:

```text
reports/handoff/YYMMDD_handoff_NN.md
```

Do not create a repository-root `handoff/` or `reports/handoff/README.md`.

## Default body

```markdown
# Conversation handoff — <project / phase>

## 1. Project objective
## 2. Current system / architecture
## 3. Authority map
## 4. Accepted decisions
## 5. Rejected / superseded directions
## 6. Current repository state
## 7. Implementation status
## 8. Known problems and unresolved decisions
## 9. Current evidence / important artifacts
## 10. Next actions
## 11. Project-specific User constraints
## 12. Source pointers / raw provenance
```

A section may be short or omitted only when it genuinely has no useful content. Do not fill empty sections with `N/A` ceremony.

## Section guidance

The authority map identifies current project `AGENTS.md`, relevant concept artifacts by `concept_id`/path, workflow Skill/reference owners, scientific source/evidence authority, current collaboration authority, and active FORMAL task when any. State explicitly that the handoff is context, not design/task/scientific authority.

Accepted decisions should preserve rationale expensive to reconstruct and point to the owning authority rather than copying concept text. Rejected/superseded directions preserve only materially important alternatives and decisive reasons.

Current repository state records the default branch/HEAD, important task branches, latest relevant task/report, important changed/new files and known unintegrated work. Prefer immutable links for committed artifacts.

Implementation status separates design maturity from implementation maturity. Known problems classify at least `BLOCKER`, `OPEN DESIGN`, `IMPLEMENTATION ISSUE`, `EVIDENCE / VERIFICATION GAP`, or `OPTIONAL / FUTURE` when applicable.

Evidence lists only materially useful concepts/tasks/reports/commits/PRs/issues/scientific sources/external repositories/user-provided source filenames. Next actions give an executable continuation order and distinguish ChatGPT DIRECT work from genuinely local Codex work.

## Authoring procedure

```text
1. resolve current project/collaboration authority;
2. inspect current repository state + relevant concept/task/report artifacts;
3. resolve the newest existing handoff, if any, only for `previous_handoff`/continuity needs;
4. summarize the source conversation independently rather than copying long stretches verbatim;
5. distinguish accepted design, implementation state, evidence, and unresolved decisions;
6. create reports/handoff/YYMMDD_handoff_NN.md with canonical metadata;
7. commit/push;
8. give the User the committed path/link and minimal new-conversation start instruction when useful.
```

## Quality check

A fresh Agent should be able to recover project objective, current architecture/state, authoritative files, settled decisions/rationale, rejected directions, implemented versus designed state, unresolved decisions/owners, next actions and underlying evidence pointers from the newest handoff plus current authority.
