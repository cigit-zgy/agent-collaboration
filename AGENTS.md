# Agent Collaboration repository context

## Repository identity

This repository is the maintained first-party source repository for the
`agent-collaboration` Skill. It defines the shared User ↔ ChatGPT ↔ Codex
collaboration protocol, reusable onboarding/templates, verification/delegation
policy, and durable design conclusions for that collaboration system.

The repository itself is not a project-specific task store and must not accumulate
scientific/project decisions that belong to another repository.

## Authority and scope

User + ChatGPT own collaboration-system design. Codex executes committed,
implementation-ready local tasks and may report contradictions or missing local
prerequisites, but it must not silently redesign the collaboration protocol.

The Agent-facing operational entry is root `SKILL.md`. Detailed global policies and
reusable templates live in `references/`. Durable accepted design truth for this
repository lives in `reports/concept/`.

For repository work, use progressive disclosure:

```text
AGENTS.md
→ SKILL.md
→ only the relevant reference
→ reports/concept/README.md when durable design history/current truth is needed
→ only the relevant concept topic
```

## Source repository versus Skill distribution

This Git repository is the maintained source/maintenance repository. It may contain
maintenance assets that are not part of a portable Skill distribution bundle.

```text
maintained source repository
├── AGENTS.md
├── SKILL.md
├── references/
└── reports/

portable Skill distribution
├── SKILL.md
└── references/      # only resources required by the Skill
```

`AGENTS.md` is a persistent repository-maintenance constitution; it is not a required
portable Skill runtime file and is not deleted merely because the Skill is mature.
A distribution/installation process may omit repository-maintenance assets when they
are not required for Skill operation.

## Repository ownership

```text
SKILL.md          Agent-facing collaboration workflow/router
references/       global policies, contracts, and reusable templates
reports/concept/  durable User + ChatGPT collaboration-system conclusions
reports/chatgpt/  formal ChatGPT task specifications owned by this repository
reports/codex/    Codex execution evidence owned by this repository
```

Do not place project-specific ChatGPT tasks, Codex reports, concepts, workspaces,
scientific data, or manuscript material here. Those assets remain in the project that
owns them.

## Maintenance rules

When changing collaboration behavior:

1. Identify the single authoritative policy/reference for the concern.
2. Update root `SKILL.md` only when activation or top-level routing changes.
3. Update a reusable template only when the template contract itself changes.
4. Update the relevant concept `Current conclusion` and decision history when a
   mature durable design conclusion changes.
5. Avoid copying the same rule into multiple files; route to the authority instead.
6. Preserve backward-readable historical reports and concepts unless a deliberate
   migration is required.

Do not turn `AGENTS.md` into a copy of `SKILL.md`, `protocol.md`, verification
policies, or template bodies.

## Skill and project template boundaries

Keep these concerns distinct:

```text
project-architecture.md
= canonical responsibility map for maintained water-domain research projects

project-agents-template.md
= project repository constitution scaffold

project-skill-template.md
= project Agent-facing workflow/router scaffold; path is project-declared and need
  not be repository root

skill-agents-template.md
= maintained first-party standalone Skill repository constitution scaffold

skill-package-architecture.md
= reusable Skill package/source-repository structure and creation conditions

skill-templates/
= purpose-specific SKILL.md scaffolds
```

Capability profile does not determine whether `AGENTS.md` exists. Repository
maintenance ownership does:

- maintained standalone first-party Skill repository: root `AGENTS.md` is required;
- embedded sub-Skill inside a parent project/repository: normally inherit the nearest
  applicable parent `AGENTS.md`; add a nested one only for genuine local maintenance
  rules;
- third-party Skill: preserve upstream structure; do not inject first-party
  `AGENTS.md` conventions;
- portable distribution bundle: `AGENTS.md` is not a required Skill component.

For maintained water-domain research projects, root `AGENTS.md` is the required
project entry. Other repository responsibilities are conditional and are created
only when their real consumer exists. The canonical responsibility map is
`references/project-architecture.md`.

## Runtime

This repository is documentation/policy oriented and owns no independent project
runtime by default. Do not create a Python environment, `pyproject.toml`, scripts, or
runtime dependencies unless a real executable consumer is introduced and explicitly
approved.

## Reports and concepts

New collaboration work owned by this repository follows:

```text
reports/chatgpt/
reports/codex/
reports/concept/
```

Read `reports/concept/README.md` before loading concept topics. Concept files record
mature durable conclusions, not transcript, status chatter, or routine execution
logs. Report lifecycle and archive rules are defined by the repository's own
`references/report-concept-policy.md`.

## Hard boundaries

- Global collaboration rules belong here; project-specific truth does not.
- `SKILL.md` governs Skill operation; `AGENTS.md` governs repository maintenance.
- Source repository and portable Skill distribution are different boundaries.
- First-party standalone Skill repositories keep root `AGENTS.md` across the
  maintenance lifecycle; maturity is not a reason to delete it.
- Embedded sub-Skills do not receive redundant `AGENTS.md` files by default.
- Project architecture is responsibility-based; optional directories are not created
  for symmetry.
- User + ChatGPT design; Codex executes approved local work.
