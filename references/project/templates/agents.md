# Project AGENTS.md template

Keep project `AGENTS.md` concise and scope-local. Route global collaboration behavior through the current/pinned `agent-collaboration/SKILL.md`; do not copy collaboration manuals.

````markdown
# <PROJECT_NAME> context

## Identity

<One or two sentences: what this repository produces and owns.>

## Authority

```text
explicit User instruction
→ reports/design/                         current accepted project design, when used
→ <workflow>/SKILL.md + references        operational workflow
→ <implementation paths>                  implementation
→ tests                                   conformance/design evidence
→ <registered source/evidence path>       scientific facts when applicable
```

`CURRENT.md`, when present, is current work state/navigation only; it does not override design/task/source authority.

`reports/concept/` is chronological design history/input only and does not override `reports/design/`.

`reports/handoff/`, when present, contains exceptional conversation-only residual delta only.

Global collaboration authority:
`cigit-zgy/agent-collaboration@<COLLABORATION_REVISION>`

Runtime collaboration entry:
`SKILL.md`

Do not preload the collaboration reference tree.

## Ownership

```text
CURRENT.md          current work edge / next-action pointer when needed
reports/design/     current living design
reports/chatgpt/    durable Codex task specifications
reports/codex/      FORMAL Codex execution reports only
reports/concept/    chronological design history/input
reports/handoff/    exceptional conversation-only delta
<path>              <project-specific responsibility>
```

Every repository task delegated to Codex is first committed under `reports/chatgpt/`. Chat carries only the short immutable task locator.

`tmp/` is the project-local Agent ephemeral boundary.

## Workflow

Normal conversation resume:

```text
AGENTS.md
→ CURRENT.md
→ reports/design/README.md
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
→ reports/design/README.md
→ directly relevant current design topic(s)
→ projection
→ implementation/tests
```

Historical rationale / new design exploration:

```text
current reports/design topic
+ only exact relevant reports/concept/YYMMDD_concept_NN.md
→ User + ChatGPT adjudication
→ update reports/design/ if accepted
```

For major architecture/tool choices, use the current collaboration prior-art route before accepting changes into `reports/design/`.

Exceptional handoff recovery occurs only when `CURRENT.md` or the User points to a specific handoff.

## Runtime and tooling

<Project runtime/tooling authority and only stable common commands an Agent actually needs.>

Project-specific shared coding-Skill additions:
`<NONE OR PROJECT-OWNED IMMUTABLE COORDINATES>`

## Human / trust checkpoints

<Only genuine project-specific scientific/product/trust decisions.>

## Hard invariants

- `reports/design/` contains one current accepted design set only; no old/draft/versioned alternatives.
- If `CURRENT.md` exists, it represents only NOW; no chronological status/task history.
- Normal full-conversation replacement uses `AGENTS.md → CURRENT.md → reports/design/README.md`.
- Every Codex repository task is specified durably under `reports/chatgpt/`; no long chat-only task body.
- LOCAL-QUICK creates no `reports/codex/` report; FORMAL does.
- <Short project-wide boundary.>
````

Do not expand this template with task plans, implementation history, global collaboration rules, detailed verification policy, or copied concept/design/CURRENT/handoff manuals.
