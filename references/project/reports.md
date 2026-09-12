# Project report and governance-artifact contract

Load this reference for `reports/` layout, chronological report naming/metadata, living-design placement, and archive placement. Project-wide artifact admission/drift is owned by `governance.md`.

## Reports root

```text
reports/
├── design/      current living design authority; not chronological
├── chatgpt/     durable Codex task specifications
├── codex/       FORMAL execution evidence
├── concept/     explicit User-requested chronological design history
└── handoff/     exceptional conversation-only delta
```

No additional active report/governance family is created without a real independent owner approved by current project/collaboration authority.

## reports/design

`reports/design/` is governed by `design.md`, not chronological report rules. It may contain `README.md`, optional `00_overview.md`, and numbered current topics.

It is the one current Design tree and contains no dated versions, backups, archives, or superseded current owners.

## Chronological families

These four are chronological:

```text
reports/chatgpt/
reports/codex/
reports/concept/
reports/handoff/
```

Each is flat. Markdown filenames use exactly:

```text
YYMMDD_<family>_NN.md
```

where `<family>` is `chatgpt | codex | concept | handoff`.

Each artifact uses the common metadata envelope:

```yaml
---
artifact_type: <project_concept | chatgpt_task | codex_report | conversation_handoff>
artifact_id: <YYMMDD_family_NN>
title: <short title>
date: <YYYY-MM-DD>
project: <project>
repository: <owner/repository>
status: <family-appropriate status>
summary: >
  <compact summary>
---
```

Non-canonical names/metadata are governance drift and are normalized without rewriting historical substance.

## Concept family

A new `reports/concept/` artifact is created only after explicit User instruction under `concept.md`.

Each request creates a new dated file. Existing Concept files remain historical snapshots and are not overwritten with later reasoning.

A normal Concept persistence request is completed only when the accepted consequence is also reflected in current `reports/design/` in the same work unit.

Concept does not own scientific qualification, golden closure, test evidence, Codex execution evidence, current status, or ordinary bug-fix history.

## ChatGPT/Codex task binding

Every repository task delegated to Codex is first committed under `reports/chatgpt/`.

```text
LOCAL-QUICK → reports/chatgpt task → compact result → no reports/codex artifact
FORMAL      → reports/chatgpt task ↔ reports/codex report
```

Chat carries only the immutable task locator.

## CURRENT and handoff

`CURRENT.md` remains repository-root mutable NOW-state and points to owners rather than duplicating them.

`reports/handoff/` is exceptional only. Normal resume is:

```text
AGENTS.md → CURRENT.md → reports/design/README.md
```

## Archive

Historical retention uses one repository-root `00_archive/`. Archive is never current authority and is not loaded by default.

## Responsibility map

```text
current accepted design          → reports/design/
explicit User-requested rationale → reports/concept/
current work edge                → CURRENT.md
Codex task                       → reports/chatgpt/
FORMAL execution evidence        → reports/codex/
scientific/model facts/evidence  → scientific/model/golden owner
exceptional conversation delta   → reports/handoff/
historical retained material    → 00_archive/
```

Repository normalization uses `governance.md` + `migration.md`; structural reduction and owner consolidation precede mere path relocation.
