# agent-collaboration

Reusable operating contracts for collaboration among the User, ChatGPT, and Codex.

The framework treats repository state as durable memory and conversations as disposable working memory. The User owns scientific/product/design/tool decisions, ChatGPT owns design/direct authoring/durable task specification/acceptance review, Codex owns LOCAL execution and environment-bound verification/repair, and project tooling/CI provides mechanical evidence.

## Runtime entry

```text
AGENTS.md
→ SKILL.md
→ one primary owning reference
→ optional second owner only when genuinely needed
```

`SKILL.md` is the sole runtime routing index.

## Current reference architecture

```text
references/
├── collaboration/
│   ├── protocol.md
│   ├── execution.md
│   ├── formal.md
│   ├── implementation.md
│   ├── verification.md
│   ├── actions.md
│   ├── shared-coding-skills.md
│   ├── agents.md
│   └── templates/
│
├── project/
│   ├── architecture.md
│   ├── current.md             # CURRENT.md + normal multi-conversation resume
│   ├── migration.md           # actual project-policy migration
│   ├── reports.md
│   ├── concept.md
│   ├── design.md
│   ├── prior-art.md
│   ├── external-tools.md
│   ├── handoff.md             # exceptional conversation-only delta
│   └── templates/
│
└── skill/
    ├── development.md
    ├── writing.md
    ├── repository.md
    ├── package.md
    └── templates/
```

## Multi-conversation project model

For long-running projects:

```text
AGENTS.md
= project constitution / authority map

design/
= what we currently accept

CURRENT.md
= what we are working on now
= mutable present work edge + pointers only

reports/concept/
= how we thought / historical design reasoning

reports/chatgpt/ + reports/codex/
= durable delegated-task specification / execution evidence

reports/handoff/
= exceptional residual conversation-only delta only

Git history
= repository evolution
```

A full conversation normally ends by making accepted state repository-native and rewriting `CURRENT.md`. It does not trigger project migration and does not automatically create a handoff.

Normal fresh-conversation resume is:

```text
AGENTS.md
→ CURRENT.md
→ design/README.md when present
→ identify current concern
→ load only the directly relevant owner(s) just in time
```

Do not preload the full design tree, concept history, old ChatGPT/Codex reports, old handoffs, archive, or complete collaboration references merely to resume.

`CURRENT.md` should normally remain <= 4 KiB; above ~8 KiB is a signal that history/design/evidence or unrelated work streams have leaked into it.

## Project design model

```text
reports/concept/
= what we considered
= chronological design history/input
= never current authority

design/
= what we currently accept
= one current structured design set
= dynamic topic decomposition
```

A material concept is reduced into living design only after User + ChatGPT adjudication.

## Existing-project migration

Project-policy migration is separate from conversation resume:

```text
current collaboration SKILL.md
→ project/migration.md
→ target repository AGENTS/CURRENT/branch/HEAD/state
→ current design and only relevant history/evidence
→ migrate only drifted surfaces
```

Opening a new conversation does not by itself justify migration assessment or design reconstruction.

## Exceptional handoff

`reports/handoff/` is used only when meaningful conversation-only continuity cannot reasonably be represented in AGENTS/design/CURRENT/task/report/concept or another real owner.

A handoff is a small delta capsule, normally <= 4 KiB. No handoff is preferable to a redundant handoff.

## Codex task handoff model

Task detail lives in the repository, not the conversation.

Every repository task delegated to Codex is first committed as:

```text
reports/chatgpt/YYMMDD_chatgpt_NN.md
```

Then the User sees only a short copyable locator.

```text
LOCAL-QUICK
→ reports/chatgpt task
→ short locator
→ compact Result contract
→ no reports/codex report

FORMAL
→ reports/chatgpt task
→ short locator
→ reports/codex execution report
→ ChatGPT acceptance/integration
```

## Hot / warm / cold context

```text
HOT
project AGENTS.md
project CURRENT.md when used
project design/README.md when present
SKILL.md when collaboration intent routing is needed

WARM
one directly relevant current design/Skill/task/report owner
one primary collaboration owner when required
optional second owner only when genuinely necessary

COLD
reports/concept/ history
historical reports/chatgpt tasks
historical reports/codex reports
reports/handoff/ unless an exceptional delta is explicitly relevant
00_archive/
unrelated owners/templates
```

## Main routes

| Concern | Read |
|---|---|
| normal conversation resume | project `AGENTS.md → CURRENT.md → design/README.md` |
| ordinary implementation | `SKILL.md` → `collaboration/implementation.md` |
| LOCAL-QUICK delegation | `SKILL.md` → `collaboration/execution.md` + LOCAL-QUICK task template |
| FORMAL task/report/acceptance | `SKILL.md` → `collaboration/formal.md` + exact FORMAL template |
| verification planning | `SKILL.md` → `collaboration/verification.md` |
| GitHub Actions | `SKILL.md` → `collaboration/actions.md` |
| existing-project migration | `SKILL.md` → `project/migration.md` |
| current-work-state design | `SKILL.md` → `project/current.md` |
| current project design | `SKILL.md` → `project/design.md` + target `design/` topic |
| design-history / new concept note | `SKILL.md` → `project/concept.md` |
| exceptional conversation delta | `SKILL.md` → `project/handoff.md` |
| Skill design/testing | `SKILL.md` → `skill/development.md` |
| new project/major design | `SKILL.md` → `project/prior-art.md` → current `design/` update |

## Core principles

```text
repository carries continuity
conversation carries working memory
CURRENT.md carries only NOW
handoff carries only exceptional residual delta
```

The intended startup read set for a mature project is only `AGENTS.md + CURRENT.md + design/README.md`; useful work should begin before large historical context is loaded. If an Agent must reconstruct the prior conversation or read several large files merely to locate the current concern, that is a routing/state-design defect.
