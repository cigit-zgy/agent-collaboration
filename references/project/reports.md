# Project report and governance-artifact contract

Load this reference for `reports/` layout, report-family filenames/metadata, living-design placement, archive placement, and report cleanup/migration.

Current work state, when used, remains repository-root `CURRENT.md` under `current.md`.

## Reports root — hard constraint

A maintained project using this model may contain these direct children under `reports/`:

```text
reports/
├── design/      current living design authority; NOT a report family
├── chatgpt/     durable Codex task specifications
├── codex/       FORMAL Codex execution evidence
├── concept/     chronological design history/input
└── handoff/     exceptional conversation-only residual delta
```

`reports/design/` is special current authority. The other four are chronological report families.

Do not create additional report/governance families such as `reports/archive/`, `reports/review/`, `reports/roadmap/`, `reports/agent/`, or nested `00_archive/`.

## reports/design exception

`reports/design/` is governed by `design.md`, not by the report-family filename/metadata contract.

It may contain:

```text
README.md
00_overview.md when justified
NN_<semantic-topic>.md
```

It may be dynamically restructured by current design responsibility. It does not use dated report filenames and does not require the common report metadata envelope.

Current design/history distinction:

```text
reports/design/  = what we currently accept
reports/concept/ = how we thought / historical design input
```

There is exactly one current `reports/design/` tree. No old/draft/versioned parallel design tree is allowed.

## Chronological report families

The following rules apply only to:

```text
reports/chatgpt/
reports/codex/
reports/concept/
reports/handoff/
```

Each is flat and contains only canonical Markdown artifacts.

Every artifact uses:

```text
YYMMDD_<family>_NN.md
```

where `<family>` is:

```text
chatgpt | codex | concept | handoff
```

Do not use semantic filenames, `README.md`, nested directories, or sidecar data inside those four active families.

Every report artifact begins with at least:

```yaml
---
artifact_type: <project_concept | chatgpt_task | codex_report | conversation_handoff>
artifact_id: <YYMMDD_family_NN>
title: <short human-readable title>
date: <YYYY-MM-DD>
project: <project name>
repository: <owner/repository>
status: <family-appropriate status>
summary: >
  <one compact searchable paragraph>
---
```

`artifact_id` equals the filename stem. Family templates may require more metadata.

## ChatGPT/Codex task binding

Every repository task delegated to Codex is first committed under `reports/chatgpt/` with:

```yaml
execution_mode: local_quick | formal
```

LOCAL-QUICK:

```text
reports/chatgpt/YYMMDD_chatgpt_NN.md
→ Codex local execution
→ compact Result contract
→ no reports/codex artifact
```

FORMAL:

```text
reports/chatgpt/YYMMDD_chatgpt_NN.md
↔ reports/codex/YYMMDD_codex_NN.md
```

The committed task is the sole task-specific execution specification; chat carries only a short locator.

Maintained Skill behavior changes still follow:

```text
reports/design/ current authority
→ SKILL.md + references
→ committed ChatGPT task
→ Codex implementation/verification
```

## Concept journal

`reports/concept/` is historical/exploratory design input, never current design authority. It may identify affected living-design topics with `design_topics`, but one concept note does not imply one design file.

## CURRENT.md is not under reports

`CURRENT.md` remains repository-root mutable NOW-state because it is the low-cost multi-conversation resume pointer, not design/history/report evidence.

It points to exact `reports/design/`, task, report, and Skill owners rather than duplicating them.

## Handoff — exceptional only

`reports/handoff/` is not the normal resume mechanism. Create a handoff only when meaningful conversation-only continuity cannot reasonably be represented in AGENTS/CURRENT/design/task/report/concept or another real owner.

Normal resume is:

```text
AGENTS.md → CURRENT.md → reports/design/README.md → just-in-time owner
```

No handoff is preferable to a redundant handoff.

## Archive

Historical retention uses exactly one repository-root:

```text
00_archive/
```

Archive is never current authority and is never loaded by default. Do not create `reports/archive/` or nested `*/00_archive/`.

Do not archive superseded living-design copies merely for convenience; Git history plus `reports/concept/` preserve design evolution.

## Responsibility summary

```text
current accepted design        → reports/design/
current active work edge       → CURRENT.md when justified
historical design reasoning    → reports/concept/
Codex task specification       → reports/chatgpt/
FORMAL execution evidence      → reports/codex/
exceptional conversation delta → reports/handoff/
historical retained material  → 00_archive/
```

## Migration / cleanup

When normalizing an existing project:

```text
1. inspect current authority and Git history;
2. move the one current living-design tree from root design/ to reports/design/ when needed;
3. update AGENTS/CURRENT/Skill/task pointers to reports/design/;
4. preserve current ChatGPT tasks, FORMAL Codex reports, concept history and valuable exceptional handoffs;
5. normalize only the four chronological report families to dated flat Markdown artifacts;
6. keep reports/design/ under design.md semantics, including README.md and numbered topic files;
7. establish/update CURRENT.md only when multi-conversation resume cost justifies it;
8. remove duplicate status/roadmap authorities and move justified historical sidecar evidence to root 00_archive/;
9. verify reports/ contains only design + the four recognized report families.
```

A path migration must not rewrite project-specific scientific/product design semantics merely to modernize layout.
