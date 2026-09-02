---
id: 04
title: Canonical Skill Package Architecture
status: active
created: 2026-09-02
updated: 2026-09-02
authority: global
scope: first-party Skill package structure, purpose profiles, progressive disclosure, and initialization rules
supersedes: null
related_tasks: []
---

# Canonical Skill Package Architecture

## Current conclusion

A reusable Skill is a bounded capability package, not a general research or software
project. Its only structurally required file is root `SKILL.md`. Supporting
`references/`, `scripts/`, and `assets/` are optional and exist only when the
capability has real on-demand knowledge, deterministic operations, or reusable
resources. First-party engineering extensions such as `tests/`, `pyproject.toml`,
and human-facing `README.md` are also conditional rather than mandatory.

The canonical package is:

```text
<skill-name>/
├── SKILL.md              # required
├── references/           # optional
├── scripts/              # optional
├── assets/               # optional
├── tests/                # optional first-party verification
├── pyproject.toml        # optional independent Python runtime authority
└── README.md             # optional human-facing documentation
```

No optional directory is created merely for symmetry or future possibility.

First-party Skill creation uses purpose profiles rather than one oversized template:

```text
documentation
executable
asset-oriented
composite/router
```

The canonical architecture is documented in
`references/skill-package-architecture.md`. Purpose-specific `SKILL.md` scaffolds
live under `references/skill-templates/`.

Skill discovery and operation use progressive disclosure:

```text
name/description
→ SKILL.md
→ only relevant references/scripts/assets
→ execute only the active branch
```

Repository ownership is a separate concern governed by
`references/skill-repository-policy.md`.

## Decision history

### 2026-09-02

#### Conclusion

The Skill development standard is split into three independent concerns:

```text
skill-repository-policy.md
= ownership, local/GitHub placement, first-party vs third-party

skill-package-architecture.md
= package contents and creation conditions

skill-templates/
= purpose-specific SKILL.md scaffolds
```

A first-party Skill is initialized by defining its capability boundary and trigger,
choosing the smallest real purpose profile, creating `SKILL.md`, and adding only
those optional resources with real consumers.

The purpose profiles are:

- Documentation Skill: primarily instructions/standards; usually `SKILL.md` plus
  optional `references/`.
- Executable Skill: Agent guidance plus deterministic code; may add `scripts/`,
  relevant `tests/`, and `pyproject.toml` only when it owns an independent runtime.
- Asset-oriented Skill: artifact generation/manipulation using reusable templates,
  style files, or static resources; uses `assets/` only when such resources exist.
- Composite/router Skill: routes among bounded downstream Skills or workflow
  branches; stays thin and does not duplicate downstream procedures.

A project-level root Skill is a special composite/router case and continues to use
`references/project-skill-template.md` because it also routes project concepts,
project lifecycle/trust state, and project runtime identity.

#### Rationale

A single mandatory directory tree causes empty folders, unnecessary runtimes, and
speculative abstractions. A minimal core plus conditional extensions preserves
portability and progressive disclosure while allowing executable first-party Skills
to use normal software-engineering verification where it is actually needed.

Separating package architecture from repository ownership also prevents two distinct
questions from being conflated: where a Skill is maintained versus what files that
Skill should contain.

#### Boundary

This concept governs reusable Skill packages. It does not define the architecture of
a full scientific/research project, which may contain multiple Skills plus data,
workspaces, experiments, manuscripts, reports, and production software.

It also does not authorize normalization of third-party Skills to the first-party
layout; upstream third-party structure remains authoritative unless an explicit
adapter is needed.

#### Impact

- `references/skill-package-architecture.md`
- `references/skill-templates/`
- `references/skill-repository-policy.md`
- `SKILL.md` onboarding/routing
- future first-party Skill initialization and audits

#### Related tasks

None. User + ChatGPT settled the architecture and ChatGPT applied it directly through
connected repository tooling because no local-machine execution was required.
