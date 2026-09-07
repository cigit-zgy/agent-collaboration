# Project conversation handoff contract

Load this reference for conversation migration/recovery semantics, handoff authority, chronology, and staleness reconciliation. Report/archive placement and filename/metadata rules are owned by `reports.md`. When authoring a new handoff, also load `templates/handoff.md`.

Project-policy migration to a newer collaboration architecture is a different concern owned by `migration.md`.

## Purpose and authority

A handoff preserves enough non-repository continuity that a new ChatGPT context can resume work without reconstructing the entire prior conversation. It is a context-recovery artifact, not design authority, task authority, scientific source authority, implementation evidence, or a substitute for project-policy migration.

```text
design/          = current accepted project design authority, when used
reports/concept/ = chronological design exploration/history
reports/chatgpt/ = committed FORMAL specification
reports/codex/   = FORMAL execution/verification evidence
reports/handoff/ = conversation continuity/context
```

If a handoff conflicts with current project authority or repository state, current authority/state wins.

## Trigger

Create a handoff only when materially true:

```text
User explicitly requests conversation migration
current conversation is becoming too large to continue reliably
work intentionally moves to a new conversation/session
future resume would otherwise lose meaningful non-repository context
```

It is a conversation checkpoint, not a running diary and not a mandatory prerequisite for project-policy migration.

If the repository already contains enough current authority/state for a new conversation and only collaboration-policy migration is needed, use `migration.md` + the compact migration bootstrap instead of manufacturing a large handoff.

## Ownership

ChatGPT is the primary handoff author because the source conversation may contain User + ChatGPT rationale, rejected directions, unresolved decisions, and continuity state not yet recoverable elsewhere. For repository-backed projects, ChatGPT should make durable state repository-native first when connected capability is sufficient, then keep the handoff focused on remaining continuity.

Codex may read a handoff for background but never treats it as current design/task/scientific authority.

## Stable layout and filename

Handoffs live only here:

```text
reports/handoff/YYMMDD_handoff_NN.md
```

There is no repository-root `handoff/` directory and no `reports/handoff/README.md` exception. Every handoff obeys the common `reports.md` YAML metadata envelope plus the family-specific fields in `templates/handoff.md`.

Issued handoffs are historical snapshots. Do not rewrite old handoff body semantics to match later design/implementation. Create a new handoff for the next migration.

## Current handoff discovery

Normal recovery selects the newest valid handoff by canonical filename chronology and verifies its metadata. `previous_handoff` provides explicit history linkage when present.

```text
project AGENTS.md
→ newest valid reports/handoff/YYMMDD_handoff_NN.md
→ re-resolve current collaboration/project authorities
→ inspect current repository HEAD/state relevant to resumed work
→ continue
```

Do not preload older handoffs. Older handoffs are history drill-down only when the newest handoff points to an unresolved historical rationale or the User asks for reconstruction.

## Authoring route

When creating a new handoff, read exactly:

```text
handoff.md
+ templates/handoff.md
```

Do not load old handoffs unless current recovery genuinely depends on them.

## Recovery validation

A current handoff plus current project authority should let a fresh Agent recover only the continuity that is not already cheap to obtain from repository-native owners, including when relevant:

```text
project objective
current active work edge
authoritative current files
settled decisions/rationale not obvious from current design
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
handoff design pointers are still current
handoff open questions are still unresolved
handoff task branch is still active
```

## Cold-path rule

Normal project execution does not load handoff authoring templates or historical handoffs. Conversation recovery loads only the newest valid handoff; authoring loads the core contract plus one template.
