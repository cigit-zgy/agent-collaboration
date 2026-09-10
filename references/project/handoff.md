# Exceptional conversation-handoff contract

Load this reference only when meaningful conversation-only continuity would otherwise be lost during a conversation switch and cannot reasonably be represented in current repository-native owners.

Normal multi-conversation resume/current work state is owned by `current.md`. Project-policy migration is owned by `migration.md`. Report placement/naming is owned by `reports.md`. When authoring an exceptional handoff, also load `templates/handoff.md`.

## Core rule

`reports/handoff/` is **not** the default way to resume a long-running project.

Normal sequential conversation replacement uses:

```text
old conversation
→ make accepted state repository-native
→ rewrite CURRENT.md to NOW
→ end

new conversation
→ AGENTS.md
→ CURRENT.md
→ design/README.md when present
→ just-in-time owner loading
```

Create a handoff only for residual context that is both:

```text
material to continuation
AND not safely/appropriately representable in AGENTS/design/CURRENT/task/report/concept or another real repository owner
```

No handoff is preferable to a redundant handoff.

## Authority

```text
design/          = current accepted project design authority
CURRENT.md       = current work edge / resume pointer
reports/concept/ = historical design reasoning
reports/chatgpt/ = durable Codex task specification
reports/codex/   = FORMAL execution evidence
reports/handoff/ = exceptional conversation-only delta
```

A handoff never overrides current design, task, scientific source authority, CURRENT, or actual repository state.

## Valid triggers

Examples:

```text
an important User intention is still only in conversation and cannot yet be safely written elsewhere
an unresolved comparison/decision needs continuity but is not yet accepted design
conversation-specific provenance or ordering would be expensive/impossible to reconstruct from repository artifacts
```

The following alone are not triggers:

```text
conversation is full
project is large
project spans many conversations
there are many completed tasks/reports
collaboration policy changed
new conversation is being opened
```

A full conversation normally causes a `CURRENT.md` checkpoint, not a handoff.

## Content boundary

A handoff is a delta capsule. It may contain only the few residual facts needed by the next conversation.

Do not copy:

```text
project objective already in AGENTS/README
design semantics already in design/
current work edge already in CURRENT.md
concept history
full task/report bodies
test matrices
commit catalogues
architecture summaries
old handoffs
conversation transcript
```

Point to owners when a pointer is needed.

## Size discipline

Normal exceptional handoff target:

```text
<= 4 KiB
```

Above roughly 8 KiB, review for duplicated repository-native material before issuing. These are architecture signals, not parser quotas.

## Authoring route

Before authoring:

```text
1. update accepted design/current task/report state in its real owner;
2. rewrite CURRENT.md to the actual current work edge when the project uses it;
3. identify the residual conversation-only delta;
4. if residual delta is empty, create no handoff;
5. otherwise create one canonical reports/handoff/YYMMDD_handoff_NN.md using the template;
6. commit/push and give the User only a short resume locator.
```

Do not reread old handoffs merely to compose a new one.

## Recovery

When CURRENT explicitly points to an exceptional handoff, or the User supplies one:

```text
AGENTS.md
→ CURRENT.md when present
→ that one handoff
→ current repository authority/state
→ continue
```

Do not chain through `previous_handoff` by default. Previous coordinates are provenance only.

## Staleness

A handoff is a snapshot/delta at a repository coordinate. On resume, reconcile it with current authority/state. If its statement is now durable or superseded elsewhere, use the current owner and ignore the stale handoff statement.

## Completion

A handoff is well formed when removing all text already recoverable from current repository owners still leaves the exact residual continuity needed by the next conversation. If nothing remains, no handoff should exist for that switch.
