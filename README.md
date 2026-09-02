# agent-collaboration

Reusable operating contracts for collaboration among the User, ChatGPT, and Codex.

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

The three reference families answer different questions:

```text
collaboration = how User, ChatGPT, and Codex work together
project       = how a maintained project is organized and connected
skill         = how a Skill is owned, packaged, written, and maintained
```

The tree above is the collaboration repository's own reference organization. `references/project/architecture.md` does not prescribe one canonical filesystem for downstream projects.

## Authority model

This repository's current operational authority lives in `references/`. Its `reports/concept/` directory records collaboration decision history/rationale rather than runtime policy.

Maintained scientific projects may use a different concept role: when their `AGENTS.md` declares `reports/concept/` as design authority, project Skills/references are operational projections of that accepted design. See `references/project/concept.md`.

## Codex execution modes

`references/collaboration/protocol.md` distinguishes:

```text
routine local execution
= bounded, ephemeral local inspection/test/diagnosis without repository mutation or durable audit artifacts

formal delegated task
= repository-changing, durable, long/multi-step, risk-sensitive, or audit-chain work
```

Formal task launch text is part of `references/collaboration/templates/chatgpt-task.md`; it is not a separate contract.

## Normal reading path

```text
AGENTS.md
→ SKILL.md
→ one owning reference
```

Do not load the whole reference tree for ordinary work.
