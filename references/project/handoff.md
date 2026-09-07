# Project conversation handoff contract

Load this reference for conversation migration/recovery semantics, handoff authority, the current-handoff index, and staleness reconciliation.

When **authoring** a new handoff, `SKILL.md` also routes directly to `templates/handoff.md`. Recovery does not need the template.

## Purpose and authority

A handoff preserves enough project state that a new ChatGPT context can resume work without reconstructing the entire prior conversation.

It is a **context-recovery artifact**, not design authority, task authority, scientific source authority, or implementation evidence.

```text
reports/concept/   = accepted project design authority, when declared
reports/chatgpt/   = committed FORMAL specification
reports/codex/     = FORMAL execution/verification evidence
reports/handoff/   = conversation continuity/context
```

If a handoff conflicts with current project authority or repository state, current authority/state wins. The handoff records what the prior conversation understood at a specific repository revision.

## Trigger

Create a handoff when materially true:

```text
User explicitly requests conversation migration
current conversation is becoming too large to continue reliably
work intentionally moves to a new conversation/session
future resume would otherwise require substantial reconstruction
```

Do not create one after every routine task/message. It is a migration checkpoint, not a running diary.

## Ownership

ChatGPT is the primary handoff author because the source conversation contains User + ChatGPT rationale, rejected directions, unresolved decisions, and continuity state.

For a repository-backed project, ChatGPT should create/commit the handoff directly when connected repository capability is sufficient. Do not delegate authorship to Codex merely because Codex also performs local execution.

Codex may read the current handoff for background when routed there by project `AGENTS.md`, a FORMAL task, or the User. It never overrides current task/project/design/scientific authority.

## Stable layout

Create this only on the first real migration:

```text
reports/handoff/
├── README.md
├── YYMMDD_handoff_01.md
├── YYMMDD_handoff_02.md
└── ...
```

Filename:

```text
YYMMDD_handoff_NN.md
```

Issued handoffs are historical snapshots. Do not rewrite old ones to match later design/implementation; create a new handoff for the next migration.

## Handoff index — required navigation surface

`reports/handoff/README.md` is a small navigation index only, not a second authority/status database.

Keep it approximately:

```markdown
# Conversation handoff index

Current handoff: `YYMMDD_handoff_NN.md`

Purpose: context recovery only; current project authority remains in AGENTS/concept/task/source artifacts.

## History

- `YYMMDD_handoff_NN.md` — <short scope/date note>
- `...`
```

Update `Current handoff` whenever a new handoff is committed. Keep history deterministic/newest-first.

Do not duplicate design rules, task status, or handoff prose in the index.

## Fast recovery route

For a new ChatGPT conversation/session:

```text
project AGENTS.md
→ reports/handoff/README.md
→ current handoff only
→ re-resolve current collaboration/project authorities
→ inspect current repository HEAD/state relevant to resumed work
→ continue
```

The current handoff should be substantially self-contained. A new conversation MUST NOT need every older handoff to understand the current project.

Older handoffs are history drill-down only when the current handoff points to an unresolved historical rationale or the User asks for reconstruction.

For Codex:

```text
FORMAL task / project AGENTS
→ current task/project authority first
→ current handoff only when additional context is needed
```

Codex does not preload all handoffs for every task.

## Authoring route

When creating a new handoff, read exactly:

```text
handoff.md                # authority/index/recovery/lifecycle
+ templates/handoff.md    # metadata/body/size/authoring checklist
```

Do not load old handoffs unless current migration evidence genuinely depends on them.

## Recovery validation

A current handoff plus current project authority should let a fresh Agent recover:

```text
project objective
current architecture/state
authoritative files
settled decisions + rationale
rejected directions
implemented versus only designed state
unresolved decisions + owners
next actions
underlying evidence pointers
```

If this requires reading several older handoffs or reconstructing the source conversation, the current handoff is insufficient.

## Staleness and reconciliation

A handoff is a snapshot at `repository_head` and creation time. On resume, reconcile it against current repository/authority state before substantive changes.

Do not silently assume:

```text
handoff repository_head == current HEAD
handoff concept pointers are still current
handoff open questions are still unresolved
handoff task branch is still active
```

Use the handoff to recover context; use current authority to determine truth now.

## Cold-path rule

Normal project execution does not load handoff authoring templates or historical handoffs. Conversation recovery loads only the current handoff; authoring loads the core contract plus one template.
