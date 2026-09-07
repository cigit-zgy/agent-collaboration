# Project migration contract

Load this reference when an existing repository must be migrated to the current `agent-collaboration` project model.

This is **project-policy migration**, not ordinary conversation handoff. Conversation continuity is owned separately by `handoff.md`.

## Purpose

Project migration updates an existing repository so its current authority, routing, living design, reports, Skill projection, and execution surfaces conform to the current collaboration model **without reconstructing the whole historical conversation or rereading the whole repository**.

The migration prompt is a map, not a manual. Repository-native artifacts remain the system of record.

## Core distinction

```text
conversation handoff
= move ongoing work to a new ChatGPT context
= preserve non-repository continuity
= owned by handoff.md

project migration
= move an existing repository onto current collaboration architecture/policy
= reconcile current repository state against current collaboration
= owned by migration.md
```

A project migration may happen inside the same conversation, after a conversation handoff, or in a new conversation using the bootstrap template below.

## Context-minimization rule — hard boundary

Do not migrate by pasting the project's full history, all concept notes, all Codex reports, or a long prose summary into the new conversation.

The preferred model is:

```text
old conversation
→ make important non-repository decisions durable when possible
→ emit a short migration bootstrap containing coordinates + unresolved delta only

new conversation
→ resolve current collaboration authority
→ inspect current target repository state
→ load only directly relevant repository-native owners
→ migrate the drifted surfaces
```

The old conversation carries only information that is expensive or impossible to recover from the repository.

## Old-conversation closure

Before generating the bootstrap, the old conversation SHOULD make durable any material accepted state that exists only in chat and can safely be written through connected capability.

Examples:

```text
accepted design decision not yet represented in repository
→ record the historical reasoning in reports/concept/ when useful
→ update current design/ if already accepted and the project is ready for that update

important unresolved local task state
→ ensure the relevant task/report/branch coordinate is recoverable

conversation-only context still needed later
→ create/update the newest handoff only when actual conversation continuity requires it
```

Do not create a large handoff merely because project-policy migration is requested. A handoff is optional unless the conversation itself is also being retired and meaningful non-repository context would otherwise be lost.

## Migration bootstrap

The old conversation emits one fenced `text` block using `templates/migration-bootstrap.md`.

The bootstrap should normally contain only:

```text
repository identity
local repository path when known and useful
one-sentence project objective
migration objective
current project AGENTS path
current design/ state: present | absent | known stale
legacy design/source pointers that are genuinely important
newest relevant handoff, if one matters
active task/report/branch/commit coordinates, if any
current unresolved blocker/design question in 1–3 short bullets
session-only accepted decisions not yet durable, only if unavoidable
explicit scope boundary such as "do not create Codex task yet"
```

Do not summarize collaboration policy inside the bootstrap. The new conversation resolves the current collaboration repository directly.

Do not summarize the entire project architecture when it is already recoverable from `design/`, current project Skills, AGENTS, or other repository-native owners.

## New-conversation recovery order

A migration begins with the smallest read set:

```text
1. resolve current cigit-zgy/agent-collaboration master
2. read current collaboration SKILL.md
3. route directly to project/migration.md
4. inspect target project root AGENTS.md and current repository branch/HEAD/state
5. inspect design/README.md if design/ exists
6. inspect only directly relevant current design topic(s)
7. inspect active task/report/handoff anchors named in the bootstrap, if any
8. read historical concept notes only when current design must be reconstructed or rationale is required
```

Do not preload:

```text
all reports/concept/
all reports/chatgpt/
all reports/codex/
all old handoffs
all collaboration references
all target project Skills/references
```

## Migration assessment first

Before broad repository edits, produce a compact migration assessment that distinguishes:

```text
ALREADY_CONFORMING
= current surface already matches the new contract

ROUTING_DRIFT
= AGENTS / Skill entry / collaboration routing is stale

DESIGN_DRIFT
= current accepted project design is missing, duplicated, stale, or still lives only in legacy concept surfaces

REPORT_DRIFT
= reports/archive layout, naming, metadata, or family semantics are stale

SKILL_PROJECTION_DRIFT
= current design is clear but project SKILL.md/references still project older semantics

IMPLEMENTATION_DRIFT
= implementation violates already-resolved current design/Skill contract

OPEN_DESIGN
= migration exposes a genuine unresolved design choice that User + ChatGPT must adjudicate
```

The assessment should name only the files/surfaces that actually need migration.

## Living-design reconstruction

When `design/` is absent or stale, do not convert every historical concept note into a design file.

Reconstruct the **single current accepted design state** using the smallest sufficient evidence set, in priority order:

```text
current project AGENTS / declared authority
→ current supported workflow SKILL.md + references
→ latest accepted repository state and implementation contracts when they unambiguously reflect accepted design
→ directly relevant incorporated/current concept notes
→ latest relevant ChatGPT task + Codex report for unresolved execution state
→ newest handoff only for conversation continuity
→ older history only when a specific unresolved rationale cannot otherwise be recovered
```

Historical concept notes remain history/input. The resulting `design/` follows `design.md` and contains one current set only.

Do not infer that implementation is correct merely because it exists. When implementation and historical design evidence conflict, classify the conflict and return genuine design ambiguity to User + ChatGPT.

## Delta migration — hard rule

Migrate only surfaces that differ materially from current collaboration.

Typical surfaces are:

```text
AGENTS.md authority/routing
repository-root design/ living-design tree
reports/ families + metadata + archive placement
project workflow SKILL.md + references
shared coding-Skill coordinates when used
GitHub Actions/verification placement when implicated
local tmp/worktree policy when stale
```

Do not rewrite already-conforming files for stylistic uniformity alone.

Do not change scientific/product semantics merely to make the repository look structurally modern.

## Execution placement

Repository-only migration that can be completed through connected GitHub capability is DIRECT ChatGPT work.

```text
repository-native policy/docs/renames/metadata/tree changes
+ no local runtime evidence required
→ ChatGPT DIRECT
```

Use Codex only when migration genuinely requires User-machine state, local filesystem/runtime evidence, or environment-bound implementation/verification.

Do not create a Codex task merely because many files need mechanical migration.

When the User explicitly says `先不用给 Codex 任务`, migration stops before Codex delegation. Complete the DIRECT migration/assessment first and report any remaining local work separately.

## Active-task reconciliation

If the bootstrap names an active task/report or a BLOCKED state, migration does not blindly continue that task.

After the project architecture/design migration:

```text
re-resolve task/report/branch against current repository state
→ determine whether the blocker is still valid under current design
→ classify as OPEN_DESIGN | IMPLEMENTATION_DRIFT | EVIDENCE_GAP | RESOLVED
→ continue only from current authority
```

An old Codex report is execution evidence, not current design authority.

## Migration completion

A project migration is complete when:

```text
current collaboration authority is correctly routed from project AGENTS
AND current project design authority is one coherent design/ tree when explicit design is used
AND reports/concept is historical/exploratory input only
AND project Skills/references project current design rather than legacy semantics
AND duplicate/parallel authority surfaces are removed or demoted
AND active task/report/blocker state has been reconciled
AND no unnecessary historical/context preload was required
AND any remaining local work is explicitly separated from completed DIRECT migration
```

## Anti-patterns

Do not use a migration prompt like:

```text
"仔细理解最新 collaboration，然后把整个项目迁移一下；下面是几百行历史背景……"
```

Do not require the new conversation to understand the old conversation before it can inspect the repository.

Do not turn the migration bootstrap into a second AGENTS file, handoff report, design document, or collaboration manual.
