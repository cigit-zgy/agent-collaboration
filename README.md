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

`SKILL.md` is the **sole runtime routing index**. There is intentionally no mandatory second index hop.

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
│   ├── reports.md              # report families / naming / archive
│   ├── concept.md              # chronological design exploration/history
│   ├── design.md               # current canonical living design + dynamic decomposition
│   ├── prior-art.md            # literature↔open-source reuse gate
│   ├── external-tools.md       # external CLI/API/schema adapters/profiles
│   ├── handoff.md              # conversation migration/recovery
│   └── templates/              # cold: AGENTS/Skill/concept/design/handoff authoring
│
└── skill/
    ├── development.md          # current design → Skill Markdown → code → tests
    ├── writing.md              # Skill/reference authoring standard
    ├── repository.md           # source/discovery/distribution
    ├── package.md              # package/resources/runtime ownership
    └── templates/              # cold: first-party Skill AGENTS template
```

## Project design model

For maintained projects using explicit design authority:

```text
reports/concept/
= what we considered
= dated design journal / historical reasoning
= may contain alternatives and unresolved ideas
= never current authority

design/
= what we currently accept
= structured living design
= one current set only
= no old/draft/versioned parallel copies
```

A material concept is reduced into the living design only after User + ChatGPT adjudication.

The `design/` file set is dynamic: topics are added, updated, split, merged, removed, or reordered according to real current design responsibilities. File count is not fixed by a universal project template.

## Hot / warm / cold context

```text
HOT
SKILL.md
project design/README.md when current design is needed

WARM
one primary collaboration owner
one directly relevant design topic
optional second owner only when genuinely necessary

COLD
reports/concept/ history unless reconstructing rationale/adjudicating a new idea
templates unless creating/reviewing that artifact
historical ChatGPT/Codex reports
old handoffs
00_archive/
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
| current project design | `SKILL.md` → `project/design.md` + target `design/` topic |
| design-history / new concept note | `SKILL.md` → `project/concept.md` |
| Skill design/testing | `SKILL.md` → `skill/development.md` |
| Skill Markdown quality | `SKILL.md` → `skill/writing.md` |
| new project/major design | `SKILL.md` → `project/prior-art.md` → current `design/` update |
| external tool adapter | `SKILL.md` → `project/external-tools.md` |
| conversation migration/recovery | `SKILL.md` → `project/handoff.md` (+ template only when authoring) |

## Design principles

### One concern, one current owner

Detailed rules live once. Other files route to the owner rather than copying the manual.

Within project `design/`, one current semantic concern has exactly one owner file.

### Direct progressive disclosure

Normal reference depth is one hop from `SKILL.md`. A reference is substantially self-contained for its concern; mandatory reference chains are avoided.

### Current design separate from history

```text
concept journal
→ adjudication
→ living design
→ Skill/reference projection
→ implementation
→ tests
```

The living design never carries old versions or rejected alternatives merely for traceability. Git history and concept notes provide that history.

### Design-first Skill development

Maintained first-party Skill behavior changes follow:

```text
current accepted design
→ SKILL.md + references
→ scripts/code/schema
→ design-probing tests
```

Tests expose general design/contract weaknesses; they do not justify task-local production patches.

### Prior art before custom design

For substantial new project/core design, inspect authoritative literature and linked/mature open-source precedents before accepting custom design into the living design tree.

### Verification claim deduplication

Codex/ChatGPT/Actions do not repeat the same expensive verification claim unless a second environment proves something materially distinct.

### Context handoff

When a project conversation is intentionally migrated, the current handoff is a high-information context snapshot, not design authority. Recovery reconciles it against current design/authority/state.

## Reports

```text
reports/concept/   chronological design journal/history
reports/chatgpt/   committed FORMAL task specifications
reports/codex/     FORMAL execution evidence
reports/handoff/   conversation migration snapshots
```

For `agent-collaboration` itself, current operational authority lives in `references/`, not historical `reports/concept/` files.

## Context-efficiency target

The intended normal read set is:

```text
thin SKILL.md
+ one primary owner
+ zero or one necessary secondary owner
+ only directly relevant current design topic(s)
+ zero historical preload
```

If an Agent must read several large files before determining the correct current owner, that is a routing/design defect.
