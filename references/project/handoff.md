# Exceptional conversation-handoff contract

Load this reference only when meaningful conversation-only continuity would otherwise be lost and cannot reasonably be represented in current repository-native owners.

Normal resume/current state is owned by `current.md`. Current design lives in `reports/design/`. Project migration is owned by `migration.md`.

## Core rule

`reports/handoff/` is not the default resume mechanism.

Normal switch:

```text
old conversation
→ make accepted state repository-native
→ rewrite CURRENT.md to NOW
→ end

new conversation
→ AGENTS.md
→ CURRENT.md
→ reports/design/README.md when present
→ just-in-time owner loading
```

Create a handoff only for residual context that is material and not safely/appropriately representable in AGENTS, `reports/design/`, CURRENT, task/report, concept, or another real owner.

No handoff is preferable to a redundant handoff.

## Authority

```text
reports/design/  = current accepted design
CURRENT.md       = current work edge / resume pointer
reports/concept/ = historical design reasoning
reports/chatgpt/ = durable Codex task specification
reports/codex/   = FORMAL execution evidence
reports/handoff/ = exceptional conversation-only delta
```

A handoff never overrides current authority/state.

## Valid triggers

Examples: an important User intention remains conversation-only and cannot yet be safely written elsewhere; an unresolved comparison needs continuity but is not accepted design; conversation-specific provenance would be expensive/impossible to reconstruct.

Conversation fullness, project size, many completed tasks, collaboration-policy change, or opening a new conversation are not sufficient triggers by themselves.

## Content boundary

Do not copy project objective, design semantics already in `reports/design/`, current edge already in CURRENT, concept history, task/report bodies, test matrices, commit catalogues, architecture summaries, old handoffs, or transcript text.

Target <= 4 KiB; above ~8 KiB, inspect for duplication.

## Authoring

```text
1. update accepted design/current task/report state in its real owner;
2. rewrite CURRENT.md when used;
3. identify residual conversation-only delta;
4. if empty, create no handoff;
5. otherwise create one reports/handoff/YYMMDD_handoff_NN.md;
6. commit/push and give only a short resume locator.
```

## Recovery

When CURRENT or the User points to an exceptional handoff:

```text
AGENTS.md
→ CURRENT.md when present
→ that one handoff
→ current repository authority/state
→ continue
```

Do not chain through older handoffs by default.

## Completion

A handoff is well formed when removing everything already recoverable from repository owners still leaves exactly the residual continuity needed by the next conversation.
