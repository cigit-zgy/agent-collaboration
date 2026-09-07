# agent-collaboration

Reusable operating contracts for collaboration among the User, ChatGPT, and Codex.

The framework supports zero-human-coding workflows: the User owns scientific/product/design/tool decisions, ChatGPT owns design/direct authoring/durable task specification/acceptance review, Codex owns LOCAL execution and environment-bound verification/repair, and project tooling/CI provides mechanical evidence.

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
│   ├── protocol.md             # roles / authority / refresh / trust
│   ├── execution.md            # DIRECT/LOCAL/FORMAL + durable Codex task handoff + Git/tmp/worktrees
│   ├── formal.md               # FORMAL report/acceptance/integration
│   ├── implementation.md       # ChatGPT-first implementation discipline
│   ├── verification.md         # levels / evidence / ChatGPT-vs-Codex placement
│   ├── actions.md              # GitHub Actions distinct hosted claims
│   ├── shared-coding-skills.md # immutable shared Skill alignment
│   ├── agents.md               # AGENTS.md writing standard
│   └── templates/              # cold: LOCAL-QUICK task + FORMAL task/report formats
│
├── project/
│   ├── architecture.md
│   ├── migration.md
│   ├── reports.md
│   ├── concept.md
│   ├── design.md
│   ├── prior-art.md
│   ├── external-tools.md
│   ├── handoff.md
│   └── templates/
│
└── skill/
    ├── development.md
    ├── writing.md
    ├── repository.md
    ├── package.md
    └── templates/
```

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

There is no long chat prompt for either mode. If task details need expansion, update the committed task file rather than appending instructions in chat.

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

Migration to a newer collaboration model is repository-native and delta-based:

```text
old conversation
→ make important session-only state durable when possible
→ short migration bootstrap only if a new conversation is taking over

new/current conversation
→ current collaboration SKILL.md
→ project/migration.md
→ target repository AGENTS + branch/HEAD/state
→ current design/ and only relevant history/evidence
→ migrate only drifted surfaces
```

Do not paste whole project history into the migration prompt.

## Hot / warm / cold context

```text
HOT
SKILL.md
active reports/chatgpt task when Codex delegation is occurring
project design/README.md when current design is needed

WARM
one primary collaboration owner
one directly relevant design topic
optional second owner only when genuinely necessary

COLD
historical reports/chatgpt tasks
reports/concept/ history unless rationale/adjudication is needed
templates unless creating/reviewing that artifact
historical FORMAL Codex reports
old handoffs
00_archive/
unrelated owners
```

## Main routes

| Concern | Read |
|---|---|
| ordinary implementation | `SKILL.md` → `collaboration/implementation.md` |
| LOCAL-QUICK delegation | `SKILL.md` → `collaboration/execution.md` + LOCAL-QUICK task template |
| FORMAL task/report/acceptance | `SKILL.md` → `collaboration/formal.md` + exact FORMAL template |
| verification planning | `SKILL.md` → `collaboration/verification.md` |
| GitHub Actions | `SKILL.md` → `collaboration/actions.md` |
| existing-project migration | `SKILL.md` → `project/migration.md` |
| current project design | `SKILL.md` → `project/design.md` + target `design/` topic |
| design-history / new concept note | `SKILL.md` → `project/concept.md` |
| Skill design/testing | `SKILL.md` → `skill/development.md` |
| new project/major design | `SKILL.md` → `project/prior-art.md` → current `design/` update |
| conversation migration/recovery | `SKILL.md` → `project/handoff.md` |

## Design principles

### One concern, one current owner

Detailed rules live once. Other files route to the owner rather than copying the manual.

### Locator, not prompt duplication

The chat handoff to Codex is only a locator to the committed task. The repository task artifact owns execution detail.

### Direct progressive disclosure

Normal reference depth is one hop from `SKILL.md`. Mandatory reference chains are avoided.

### Repository-native migration

Give the next Agent a map, not a transcript. The target repository is the system of record.

### Current design separate from history

```text
concept journal
→ adjudication
→ living design
→ Skill/reference projection
→ implementation
→ tests
```

### Design-first Skill development

```text
current accepted design
→ SKILL.md + references
→ scripts/code/schema
→ design-probing tests
```

### Verification claim deduplication

Codex/ChatGPT/Actions do not repeat the same expensive verification claim unless a second environment proves something materially distinct.

## Reports

```text
reports/chatgpt/   all durable Codex task specifications: LOCAL-QUICK + FORMAL
reports/codex/     FORMAL execution evidence only
reports/concept/   chronological design journal/history
reports/handoff/   conversation migration snapshots
```

For `agent-collaboration` itself, current operational authority lives in `references/`, not historical `reports/concept/` files.

## Context-efficiency target

```text
thin SKILL.md
+ one primary owner
+ active task artifact only when delegation occurs
+ zero historical preload
```

If an Agent must read several large files before determining the correct current owner, that is a routing/design defect.
