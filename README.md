# agent-collaboration

Reusable operating contracts for collaboration among the User, ChatGPT, and Codex.

The framework supports a zero-human-coding workflow: the User owns scientific/product/design/tool decisions, ChatGPT owns design/direct authoring/acceptance review, Codex owns LOCAL execution and environment-bound verification/repair, and project tooling/CI provides mechanical evidence.

## Entry

- `AGENTS.md` — maintenance constitution for this repository.
- `SKILL.md` — top-level collaboration router.
- `references/` — current operational policy, organized by owner.
- `reports/` — decision history, formal tasks, and execution evidence.

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
project       = how a maintained project is organized and connected
skill         = how a Skill is owned, packaged, written, and maintained
```

Within collaboration:

```text
protocol             = authority, routing, Git/task boundaries, report lookup, acceptance
implementation       = ChatGPT-first/AI-assisted code authoring + engineering discipline
shared-coding-skills = common immutable Skill authorities + ChatGPT/Codex alignment
verification         = verification levels + evidence categories + online/local placement
```

## Authority model

Current operational authority lives in `references/`. `reports/concept/` records this repository's decision history/rationale rather than runtime policy.

Maintained scientific projects may declare their own `reports/concept/` as canonical project design authority. Their model-specific scientific facts remain grounded in registered source/evidence rather than project governance documents.

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

The User is not required to write code or inspect every line. Material implementation decisions and verification evidence instead remain auditable through bounded changes, shared Skill authorities, clear contracts, tests/tooling, Codex local evidence, and ChatGPT acceptance review.

## Normal reading path

```text
AGENTS.md
→ SKILL.md
→ one owning reference
```

Do not load the whole reference tree or every installed Skill for ordinary work.
