# agent-collaboration

Reusable operating contracts for collaboration among the User, ChatGPT, and Codex.

The framework supports a zero-human-coding workflow: the User owns scientific/product/design/tool decisions, ChatGPT owns design/direct authoring/conversation handoff/acceptance review, Codex owns LOCAL execution and environment-bound verification/repair, and project tooling/CI provides mechanical evidence.

## Entry

- `AGENTS.md` — maintenance constitution for this repository.
- `SKILL.md` — top-level collaboration router.
- `references/` — current operational policy, organized by owner.
- `reports/` — decision history, formal tasks, execution evidence, and project conversation handoffs when enabled by a target project.

## Reference architecture

```text
references/
├── collaboration/
│   ├── protocol.md
│   ├── implementation.md
│   ├── shared-coding-skills.md
│   ├── verification.md
│   ├── agents.md
│   └── templates/
│       ├── chatgpt-task.md
│       └── codex-report.md
│
├── project/
│   ├── architecture.md
│   ├── concept.md
│   ├── prior-art.md
│   ├── handoff.md
│   └── templates/
│       ├── agents.md
│       └── skill.md
│
└── skill/
    ├── repository.md
    ├── package.md
    ├── writing.md
    └── templates/
        └── agents.md
```

The reference families answer different questions:

```text
collaboration = how User, ChatGPT, and Codex work together
project       = how a maintained project is designed, organized, recovered across conversations, and connected
skill         = how a Skill is owned, packaged, written, and maintained
```

Within collaboration:

```text
protocol             = authority, routing, Git/task boundaries, report lookup, acceptance
implementation       = ChatGPT-first/AI-assisted code authoring + engineering discipline
shared-coding-skills = common immutable Skill authorities + ChatGPT/Codex alignment
verification         = verification levels + evidence categories + online/local placement
```

Within project:

```text
architecture = repository ownership, runtime boundaries, project-local tmp state, handoff placement
concept      = accepted design authority and freeze/adjudication lifecycle
prior-art    = mandatory literature↔open-source search and reuse/adapt/custom-gap gate for substantial new design
handoff      = conversation migration, context snapshot schema, current-handoff index, and fast recovery route
```

## Authority model

Current operational authority lives in `references/`. `reports/concept/` records this repository's decision history/rationale rather than runtime policy.

Maintained scientific projects may declare their own `reports/concept/` as canonical project design authority. Their model-specific scientific facts remain grounded in registered source/evidence rather than project governance documents.

External prior art informs project design but does not become project authority. For new projects, core subsystems, major algorithms/architectures, and substantial tool/framework choices, the project must inspect authoritative literature and linked/mature open-source implementations before freezing a custom concept.

Project conversation handoffs are also non-authoritative: they preserve a high-information snapshot of the prior ChatGPT conversation and repository state, but current `AGENTS.md`, concept/task/source authority, and current repository state always win.

A local `.agents/skills` entry is discovery, not cross-Agent authority. Coding Skills that constrain both ChatGPT and Codex are identified by immutable repository/commit/path coordinates under `references/collaboration/shared-coding-skills.md` or an explicit project/task profile.

## Execution modes

`references/collaboration/protocol.md` defines three routes:

```text
DIRECT
= ChatGPT completes work supported by connected capability

LOCAL-QUICK
= bounded low-risk local implementation/execution with focused verification and ChatGPT acceptance review

FORMAL
= major, long, risk-sensitive, trust/public-contract, persistent-state, or release work using a committed task and durable report
```

Code authorship and verification location are decided separately. ChatGPT writes code/tests it can correctly author from repository/design/shared-Skill context; cheap available checks run online, while project-environment or time-consuming checks run through Codex locally.

Repository-changing FORMAL work defaults to a dedicated task branch/worktree, so an isolated long task does not freeze the shared default branch.

Formal task launch text lives in `references/collaboration/templates/chatgpt-task.md`.

## AI-assisted implementation

`references/collaboration/implementation.md` requires AI-generated implementation to be transparent, reviewable, maintainable, and held to the same quality standard as maintained human-authored code.

Before substantial custom implementation of a gate-triggered design, `references/project/prior-art.md` requires a prior-art review and a concept-level `REUSE | ADAPT | REFERENCE_ONLY | REJECT` decision. Existing strong implementations are understood first; custom code is reserved for the remaining justified gap.

The User is not required to write code or inspect every line. Material implementation decisions and verification evidence instead remain auditable through bounded changes, shared Skill authorities, clear contracts, tests/tooling, Codex local evidence, and ChatGPT acceptance review.

## Conversation handoff and recovery

When a project conversation is intentionally migrated or has become too large to continue reliably, `references/project/handoff.md` defines a DIRECT ChatGPT handoff artifact under:

```text
reports/handoff/YYMMDD_handoff_NN.md
```

The project also keeps a small navigation file:

```text
reports/handoff/README.md
```

which points to the current handoff. The normal recovery route is:

```text
project AGENTS.md
→ reports/handoff/README.md
→ current handoff only
→ current project/collaboration authority + current repository state
→ continue
```

Older handoffs are historical drill-down only; do not preload them all.

## Normal reading path

```text
AGENTS.md
→ SKILL.md
→ one owning reference
```

For new project/core design:

```text
AGENTS.md
→ SKILL.md
→ references/project/prior-art.md
→ governing project concept
```

For conversation migration/recovery:

```text
AGENTS.md
→ SKILL.md
→ references/project/handoff.md  # when authoring/migrating

or

AGENTS.md
→ reports/handoff/README.md
→ current handoff                # when resuming
```

Do not load the whole reference tree, every installed Skill, or every historical handoff for ordinary work.
