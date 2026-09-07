# agent-collaboration

Reusable operating contracts for collaboration among the User, ChatGPT, and Codex.

The framework supports zero-human-coding workflows: the User owns scientific/product/design/tool decisions, ChatGPT owns design/direct authoring/conversation handoff/acceptance review, Codex owns LOCAL execution and environment-bound verification/repair, and project tooling/CI provides mechanical evidence.

## Runtime entry

```text
AGENTS.md
→ SKILL.md
→ one primary owning reference
→ optional second owner only when the active concern genuinely spans both
```

`SKILL.md` is the **sole runtime routing index**. There is intentionally no mandatory `references/INDEX.md` hop.

This follows the progressive-disclosure pattern used by maintained Agent-Skill ecosystems: core trigger/routing stays in the Skill entry, specialized material loads on demand, and reference chains are avoided.

## Current reference architecture

```text
references/
├── collaboration/
│   ├── protocol.md             # roles / authority / refresh / trust
│   ├── execution.md            # DIRECT/LOCAL/FORMAL + Git/tmp/worktrees
│   ├── formal.md               # committed task/report/acceptance/integration
│   ├── implementation.md       # ChatGPT-first implementation discipline
│   ├── verification.md         # levels / evidence / ChatGPT-vs-Codex placement
│   ├── actions.md              # GitHub Actions distinct hosted claims
│   ├── shared-coding-skills.md # immutable shared Skill alignment
│   ├── agents.md               # AGENTS.md writing standard
│   └── templates/              # cold: exact FORMAL task/report formats
│
├── project/
│   ├── architecture.md         # project ownership/integration
│   ├── external-tools.md       # external CLI/API/schema adapters/profiles
│   ├── concept.md              # project design authority lifecycle
│   ├── prior-art.md            # literature↔open-source reuse gate
│   ├── handoff.md              # conversation migration/recovery
│   └── templates/              # cold: project AGENTS/Skill/handoff authoring
│
└── skill/
    ├── development.md          # concept → Skill Markdown → code → tests
    ├── writing.md              # Skill/reference authoring standard
    ├── repository.md           # source/discovery/distribution
    ├── package.md              # package/resources/runtime ownership
    └── templates/              # cold: first-party Skill AGENTS template
```

## Hot / warm / cold context

```text
HOT
SKILL.md

WARM
one primary owner
optional second owner explicitly selected by SKILL.md

COLD
templates unless creating/reviewing that artifact
reports/concept decision history
historical ChatGPT/Codex reports
old handoffs
unrelated owners
```

Ordinary use should never require browsing the whole repository before discovering the relevant contract.

## Main routes

| Concern | Read |
|---|---|
| ordinary implementation | `SKILL.md` → `collaboration/implementation.md` |
| verification planning | `SKILL.md` → `collaboration/verification.md` |
| GitHub Actions | `SKILL.md` → `collaboration/actions.md` |
| local Git/tmp/worktree | `SKILL.md` → `collaboration/execution.md` |
| FORMAL task/report/acceptance | `SKILL.md` → `collaboration/formal.md` + exact template only when needed |
| Skill design/testing | `SKILL.md` → `skill/development.md` |
| Skill Markdown quality | `SKILL.md` → `skill/writing.md` |
| new project/major design | `SKILL.md` → `project/prior-art.md` + target project concept |
| external tool adapter | `SKILL.md` → `project/external-tools.md` |
| conversation migration/recovery | `SKILL.md` → `project/handoff.md` (+ template only when authoring) |

## Design principles

### One concern, one owner

Detailed rules live once. Other files route to the owner rather than copying the manual.

### Direct progressive disclosure

Normal reference depth is one hop from `SKILL.md`. A reference is substantially self-contained for its concern; mandatory reference chains are avoided.

### Concept-first Skill development

Maintained first-party Skill behavior changes follow:

```text
accepted concept/design
→ SKILL.md + references
→ scripts/code/schema
→ design-probing tests
```

Tests are used to expose general design/contract weaknesses, not to optimize production code around one current fixture.

### Prior art before custom design

For substantial new project/core design, inspect authoritative literature and linked/mature open-source precedents before freezing a custom concept.

### Verification claim deduplication

Codex/ChatGPT/Actions do not repeat the same expensive verification claim unless a second environment proves something materially distinct.

### Context handoff

When a project conversation is intentionally migrated, the current handoff is a high-information context snapshot, not design authority. Recovery reads only the current handoff plus current authority/state.

## Reports

```text
reports/concept/   collaboration decision history/rationale
reports/chatgpt/   historical committed FORMAL task specifications
reports/codex/     historical FORMAL execution evidence
```

For `agent-collaboration` itself, current operational authority lives in `references/`, not historical `reports/concept/` files.

## Context-efficiency target

The intended normal read set is:

```text
thin SKILL.md
+ one primary owner
+ zero or one necessary secondary owner
+ zero historical preload
```

If an Agent must read several large collaboration files before determining the correct owner, that is a routing/design defect.
