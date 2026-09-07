# Project AGENTS.md template

Read `../../collaboration/agents.md` first. Keep project `AGENTS.md` concise and scope-local: declare project authority, ownership, workflow entry, tooling, and genuine trust boundaries. Route global collaboration behavior through the current/pinned `agent-collaboration/SKILL.md`; do not copy collaboration manuals.

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
→ <registered source/evidence path>       model/domain-specific scientific facts, when applicable
```

`reports/concept/` is chronological design exploration/history only; it does not override current `design/`.

`reports/handoff/`, when present, is conversation context only and never overrides current design/task/source authority.

Global collaboration authority:
`cigit-zgy/agent-collaboration@<COLLABORATION_REVISION>`

Runtime collaboration entry:
`SKILL.md`

Do not preload the collaboration reference tree. Resolve the active intent through that Skill and read only the selected owner(s).

## Ownership

```text
design/             current living design, when used
reports/chatgpt/    durable Codex task specifications: LOCAL-QUICK + FORMAL
reports/codex/      FORMAL Codex execution reports only
reports/concept/    chronological design history/input
<path>              <responsibility>
```

Every repository task delegated to Codex is first committed under `reports/chatgpt/`. Chat carries only the short immutable task locator; detailed task instructions do not live in the conversation.

`tmp/` is the project-local Agent ephemeral boundary; detailed local execution/Git/worktree semantics come from the collaboration `execution.md` owner selected through `SKILL.md`.

## Workflow

Routine:

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
+ only relevant reports/concept/YYMMDD_concept_NN.md
→ User + ChatGPT adjudication
→ update design/ if accepted
```

For a new project/core subsystem or major algorithm/architecture/tool choice, use the current collaboration prior-art route before accepting the change into `design/`.

When `reports/handoff/` exists, context recovery reads only the newest valid handoff, then re-resolves current authority/state.

## Runtime and tooling

<Project runtime/tooling authority and only stable common commands an Agent actually needs.>

Project-specific shared coding-Skill additions:
`<NONE OR PROJECT-OWNED IMMUTABLE COORDINATES>`

Global implementation, verification, Actions, Git/local execution, Codex delegation, prior-art, living-design, external-tool, report, and handoff policy is discovered through the current/pinned collaboration `SKILL.md`.

## Human / trust checkpoints

<Only genuine project-specific scientific/product/trust decisions.>

## Hard invariants

- `design/` contains one current accepted design set only; no old/draft/versioned alternatives.
- Every Codex repository task is specified durably under `reports/chatgpt/`; no long chat-only task body.
- LOCAL-QUICK creates no `reports/codex/` report; FORMAL does.
- <Short project-wide boundary.>
````

Do not expand this template with task plans, implementation history, global collaboration rules, detailed verification policy, or copied concept/design/handoff manuals. Point to the owning project artifact or collaboration route instead.
