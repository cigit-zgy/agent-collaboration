# Project report and archive contract

Load this reference for repository report-family layout, report filenames/metadata, archive placement, and report cleanup/migration.

Current accepted project design is outside `reports/` and is owned by repository-root `design/`. Current collaboration/work edge, when used, is outside `reports/` and owned by repository-root `CURRENT.md` under `current.md`.

## Reports root — hard constraint

When a maintained project uses `reports/`, it may contain only these four direct child directories:

```text
reports/
├── chatgpt/
├── codex/
├── concept/
└── handoff/
```

Each family directory is flat and contains only canonical Markdown artifacts. Supporting evidence that must be retained belongs in the single repository-root `00_archive/` or another explicitly declared non-report owner.

Responsibilities are fixed:

```text
reports/chatgpt/ = durable ChatGPT-authored Codex task specifications for LOCAL-QUICK and FORMAL
reports/codex/   = FORMAL Codex execution/verification reports only
reports/concept/ = chronological design exploration/history; never current design authority
reports/handoff/ = exceptional conversation-only residual delta; not normal resume state

design/          = current accepted structured project design
CURRENT.md       = current work edge / resume pointer when the project uses current-state tracking
```

LOCAL-QUICK deliberately has no `reports/codex/` artifact. FORMAL has both a ChatGPT task and bound Codex report.

A roadmap, backlog, discussion diary, review log, integration note, qualification note, current-status diary, or historical implementation record is not a fifth report family.

## Execution ownership for report normalization

```text
connected repository capability sufficient
AND no User-machine/runtime evidence required
→ DIRECT ChatGPT

local filesystem/runtime/tool evidence genuinely required
→ LOCAL-QUICK or FORMAL under execution.md
```

Do not create Codex work merely for deterministic repository-side normalization that ChatGPT can complete directly.

## Filename contract — hard constraint

Every Markdown artifact under `reports/` uses exactly:

```text
YYMMDD_<family>_NN.md
```

where `<family>` is:

```text
chatgpt | codex | concept | handoff
```

`NN` is a two-digit sequence within the same date + family. Do not use semantic filenames, `README.md`, `index.md`, or another naming pattern inside active `reports/`.

## Common metadata envelope — required

Every report Markdown file begins with at least:

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

`artifact_id` equals the filename stem. Family templates may require additional metadata.

## ChatGPT task specifications

Every repository task delegated to Codex is first committed under `reports/chatgpt/`.

Task metadata identifies execution mode:

```yaml
execution_mode: local_quick | formal
```

Templates:

```text
LOCAL-QUICK → references/collaboration/templates/local-quick-task.md
FORMAL      → references/collaboration/templates/chatgpt-task.md
```

The committed task is the sole task-specific execution specification. Chat only carries a short immutable locator.

### LOCAL-QUICK binding

```text
reports/chatgpt/YYMMDD_chatgpt_NN.md
→ Codex local execution
→ compact Result contract returned in chat
```

No `reports/codex/` report is created.

### FORMAL binding

```text
reports/chatgpt/YYMMDD_chatgpt_NN.md
↔ reports/codex/YYMMDD_codex_NN.md
```

The formal task binds the exact expected Codex report path.

For maintained Skill behavior changes, both modes still follow:

```text
current accepted design/
→ committed SKILL.md + references
→ committed ChatGPT task
→ Codex implementation/verification
```

## Concept-journal metadata

A concept note is historical/exploratory design input, not design authority. It may identify affected current design topics:

```yaml
status: <open | incorporated | rejected | superseded | recorded>
design_topics:
  - <design_id>
```

Detailed concept semantics are owned by `concept.md`.

## CURRENT.md is not a report

`CURRENT.md` is a repository-root mutable current-state pointer owned by `current.md`.

It may summarize only the present work edge and link to exact task/report/design owners. It must not preserve report history, duplicate report bodies, or act as a fifth report family.

When the active task/report state changes, CURRENT may be rewritten to point to the new adopted work edge. Git history preserves earlier CURRENT states.

## Handoff discovery — exceptional only

Handoffs live only in `reports/handoff/` and are not the normal multi-conversation resume mechanism.

A handoff is created only when meaningful conversation-only continuity would otherwise be lost and cannot reasonably be represented in AGENTS/design/CURRENT/task/report/concept or another real owner.

Normal resume is owned by `current.md`:

```text
AGENTS.md → CURRENT.md → design/README.md → just-in-time current owner
```

When an exceptional handoff exists, CURRENT or the User may point to the one relevant handoff. Do not traverse historical handoff chains by default.

## Archive — single-root hard constraint

A maintained repository uses exactly one archive location when archival retention is needed:

```text
<repository-root>/00_archive/
```

Do not create `archive/` or nested `*/00_archive/` directories.

Archive is history only: never current design/task/report/runtime authority and never loaded by default. If retention has no recovery, legal, provenance, or audit value, delete rather than archive.

Do not store superseded living-design copies in archive merely for convenience; Git history and `reports/concept/` preserve design evolution.

## Roadmaps and duplicate status files

```text
current accepted architectural direction → design/
current active work edge                  → CURRENT.md when justified
historical reasoning / explored ideas     → reports/concept/
execution backlog                         → issues/tasks or declared work-management surface
```

Do not create a parallel current-status report or roadmap that duplicates `CURRENT.md` or `design/`.

## Migration / cleanup rule

When normalizing an existing project:

```text
1. inspect current authority and Git history;
2. preserve current ChatGPT tasks, FORMAL Codex reports and exceptional handoffs with real value;
3. normalize report filenames and required metadata;
4. classify reports/concept as chronological design history;
5. establish/update repository-root design/ separately when explicit living design is used;
6. establish/update CURRENT.md only when long-running/multi-conversation resume cost justifies it;
7. delete obsolete duplicate status/roadmap files when another owner already exists;
8. move retained report-history/sidecar evidence into root 00_archive/reports/... when justified;
9. verify reports/ contains only the four allowed flat families.
```

Do not rewrite historical scientific/task/design reasoning merely to modernize formatting. Backfill only factual metadata recoverable from path/content/Git history.
