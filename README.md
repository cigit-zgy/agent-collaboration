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
│       ├── codex-launch.md
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

## Authority model

This repository's current operational authority lives in `references/`. Its `reports/concept/` directory records collaboration decision history/rationale rather than runtime policy.

Maintained scientific projects may use a different concept role: when their `AGENTS.md` declares `reports/concept/` as design authority, project Skills/references are operational projections of that accepted design. See `references/project/concept.md`.

## Normal reading path

```text
AGENTS.md
→ SKILL.md
→ one owning reference
```

Do not load the whole reference tree for ordinary work.
