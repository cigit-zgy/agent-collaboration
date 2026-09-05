---
id: 09
title: Conversation handoff and context recovery decisions
status: active
created: 2026-09-05
updated: 2026-09-05
role: decision_history
operational_authority:
  - references/project/handoff.md
  - references/project/architecture.md
  - references/project/concept.md
  - references/project/templates/agents.md
related_tasks: []
---

# Conversation handoff and context recovery — decision history

## Context

Maintained research/software projects may span multiple ChatGPT conversations. A conversation can become too large to continue reliably, or the User may intentionally migrate work to a new conversation while expecting the new context to recover the accepted decisions, rejected alternatives, repository state, implementation status, unresolved questions, and next actions without rereading the entire source conversation.

Existing durable artifacts already separate design (`reports/concept/`), FORMAL task specifications (`reports/chatgpt/`), Codex execution evidence (`reports/codex/`), scientific source/evidence, and implementation. None of those artifacts is intended to reconstruct the working context of a long User + ChatGPT discussion.

## Accepted decisions

### Dedicated context-recovery artifact

Projects may use:

```text
reports/handoff/
```

for conversation continuity. A handoff is context/evidence only; it is not design authority, task authority, scientific source authority, or execution evidence.

### Creation only on real migration

Do not pre-create a handoff directory for every project. Create `reports/handoff/` on the first real conversation migration or other material context-recovery need.

### Stable handoff files

Each migration creates a new stable Markdown file:

```text
YYMMDD_handoff_NN.md
```

Old handoffs are retained as historical snapshots and are not rewritten to represent newer design or implementation state.

### Small current-handoff index

`reports/handoff/README.md` is a navigation-only index with one explicit `Current handoff` pointer plus a compact history list. It is not a second status database or authority source.

This avoids requiring a new Agent to infer the latest file from directory ordering or read all historical handoffs.

### ChatGPT owns handoff authorship

ChatGPT is the primary handoff author because it has the source conversation context and owns design partnership with the User. Handoff creation is normally DIRECT repository work when connected GitHub access is sufficient; Codex is not the default handoff author.

Codex may read the current handoff for background when routed there, but current task/project authority always wins.

### Information-dense size target

The normal handoff target is 300–600 lines, with approximately:

```text
simple migration          250–400 lines
complex project migration 400–600 lines
major architecture phase  600–800 lines
```

This is architecture guidance rather than a parser limit. More than roughly 800 lines signals likely duplication of concept/task/report/transcript content and should be reviewed.

### Substantially self-contained latest handoff

The current handoff should be sufficient to resume the project without reading every previous handoff. Historical handoffs are drill-down sources only.

### Fixed recovery information

The handoff preserves, when relevant:

```text
project objective
current architecture/system map
authority map
accepted decisions + rationale
rejected/superseded directions
current repository state
implementation status
known problems/unresolved decisions
important evidence/artifact pointers
next actions
project-specific User constraints
source pointers/raw provenance
```

A full conversation transcript is not copied into the repository merely for completeness.

### Raw provenance

Compact YAML metadata and source pointers preserve the recoverable origin of the handoff, including repository HEAD, collaboration commit, source conversation title/time range/URL when available, previous handoff, important concept/task/report/commit links, papers/DOIs, external repositories, and important user-provided source filenames.

Conversation IDs or URLs are omitted rather than invented when unavailable.

### Reconcile before continuing

A handoff is a snapshot at one repository revision/time. A new ChatGPT/Codex context uses it for orientation, then re-resolves current project/collaboration authority and current repository state before substantive work.

### Fast reading route

When handoffs exist, project `AGENTS.md` routes recovery as:

```text
AGENTS.md
→ reports/handoff/README.md
→ current handoff only
→ current project/collaboration authority + repository state
→ normal workflow/design route
```

This keeps context recovery shallow and deterministic.

## Operational projection

Current operational owners are:

```text
references/project/handoff.md
references/project/architecture.md
references/project/concept.md
references/project/templates/agents.md
SKILL.md
```

`references/project/handoff.md` is the single detailed owner for handoff layout, index, metadata, content requirements, size guidance, creation, recovery, provenance, and staleness reconciliation.
