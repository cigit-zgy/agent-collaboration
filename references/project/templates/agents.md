# Project AGENTS.md template

Read `../../collaboration/agents.md` first. Keep project `AGENTS.md` concise and scope-local: declare project authority, ownership, workflow entry, tooling, normal resume route when used, and genuine trust boundaries. Route global collaboration behavior through the current/pinned `agent-collaboration/SKILL.md`; do not copy collaboration manuals.

````markdown
# <PROJECT_NAME> context

## Identity

<One or two sentences: what this repository produces and owns.>

## Authority

```text
explicit User instruction
→ design/                                current accepted project design, when used
→ <workflow>/SKILL.md + references       operational workflow
→ <implementation paths>                 implementation
→ tests                                  conformance/design evidence
→ <registered source/evidence path>      model/domain-specific scientific facts, when applicable
```

`CURRENT.md`, when present, is current work state/navigation only; it does not override design/task/source authority.

`reports/concept/` is chronological design exploration/history only.

`reports/handoff/`, when present, contains exceptional conversation-only residual delta only and never overrides current authority/state.

Global collaboration authority:
`cigit-zgy/agent-collaboration@<COLLABORATION_REVISION>`

Runtime collaboration entry:
`SKILL.md`

Do not preload the collaboration reference tree. Resolve the active intent through that Skill and read only the selected owner(s).

## Ownership

```text
CURRENT.md          current work edge / next-action pointer when this project needs multi-conversation resume
design/             current living design, when used
reports/chatgpt/    durable Codex task specifications: LOCAL-QUICK + FORMAL
reports/codex/      FORMAL Codex execution reports only
reports/concept/    chronological design history/input
reports/handoff/    exceptional conversation-only delta
<path>              <responsibility>
```

Every repository task delegated to Codex is first committed under `reports/chatgpt/`. Chat carries only the short immutable task locator; detailed task instructions do not live in the conversation.

`tmp/` is the project-local Agent ephemeral boundary; detailed local execution/Git/worktree semantics come from the collaboration `execution.md` owner selected through `SKILL.md`.

## Workflow

Normal conversation resume, when `CURRENT.md` is used:

```text
AGENTS.md
→ CURRENT.md
→ design/README.md when present
→ directly relevant current owner only
```

This is not project migration. Do not preload project history, the whole design tree, or old task/report/handoff files merely to resume.

Routine execution:

```text
AGENTS.md
→ <workflow>/SKILL.md
→ owning project reference/script
```

Current design / conformance:

```text
AGENTS.md
→ design/README.md
→ directly relevant current design topic(s)
→ projection
→ implementation/tests
```

Historical rationale or new design exploration:

```text
current design topic
+ only exact relevant reports/concept/YYMMDD_concept_NN.md
→ User + ChatGPT adjudication
→ update design/ if accepted
```

For a new project/core subsystem or major algorithm/architecture/tool choice, use the current collaboration prior-art route before accepting the change into `design/`.

Exceptional handoff recovery occurs only when `CURRENT.md` or the User points to a specific handoff that carries residual conversation-only context.

## Runtime and tooling

<Project runtime/tooling authority and only stable common commands an Agent actually needs.>

Project-specific shared coding-Skill additions:
`<NONE OR PROJECT-OWNED IMMUTABLE COORDINATES>`

Global implementation, verification, Actions, Git/local execution, Codex delegation, prior-art, current-state, living-design, external-tool, report, migration, and exceptional-handoff policy is discovered through the current/pinned collaboration `SKILL.md`.

## Human / trust checkpoints

<Only genuine project-specific scientific/product/trust decisions.>

## Hard invariants

- `design/` contains one current accepted design set only; no old/draft/versioned alternatives.
- If `CURRENT.md` exists, it represents only NOW; no chronological status/task history.
- Normal full-conversation replacement uses `AGENTS.md → CURRENT.md → design/README.md`, not project migration and not a default handoff.
- Every Codex repository task is specified durably under `reports/chatgpt/`; no long chat-only task body.
- LOCAL-QUICK creates no `reports/codex/` report; FORMAL does.
- <Short project-wide boundary.>
````

Do not expand this template with task plans, implementation history, global collaboration rules, detailed verification policy, or copied concept/design/CURRENT/handoff manuals. Point to the owning project artifact or collaboration route instead.
