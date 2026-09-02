# Agent Collaboration repository context

## Repository role

This is the maintained first-party source repository for the `agent-collaboration`
Skill. It defines how User, ChatGPT, and Codex collaborate and provides reusable
project/Skill onboarding contracts.

Root `AGENTS.md` governs maintenance of this repository. Root `SKILL.md` is the
Agent-facing collaboration router. They are persistent source-repository assets and
serve different purposes.

## Authority model

For this repository itself, use one current operational authority per concern:

```text
AGENTS.md
= repository-local maintenance instructions

SKILL.md
= activation and top-level routing only

references/*
= current operational collaboration/project/Skill contracts

reports/concept/*
= accepted decision history, rationale, and pointers to current operational authority

reports/chatgpt/*
= committed local-execution specifications

reports/codex/*
= execution and verification evidence
```

When this repository's concept history and an operational reference disagree, the
operational reference is current policy. Concepts explain why policy evolved; they do
not create a competing runtime authority here.

Project repositories may declare a different concept role. In maintained scientific
research projects, selected `reports/concept/*` topics may be the canonical User +
ChatGPT design specification, while project Skills/references are operational
projections of that design. This relationship is governed by
`references/report-concept-policy.md`, `references/project-integration.md`, and
`references/project-architecture.md`.

Do not conflate project design authority with model/source scientific evidence.
Project concepts may define the scientific architecture and contracts; registered
source/evidence remains the authority for model-specific scientific facts.

## Reading order

For ordinary collaboration work in this repository:

```text
AGENTS.md
→ SKILL.md
→ only the reference required by the active route
```

Read this repository's `reports/concept/README.md` and a concept topic only when
historical design rationale, supersession, or the reason behind a current contract is
materially needed.

For a target project, follow that project's declared authority model. Routine runtime
may stay `AGENTS → workflow Skill → sub-Skill → reference`; design/redesign/audit work
may require the project's governing design-authority concept first.

## Skill source, discovery, and distribution

Keep these boundaries distinct:

```text
maintained first-party source
/Users/wenv/Documents/skills/<skill-name>/

Codex local discovery
$HOME/.agents/skills/<skill-name>
  → normally a symlink to the maintained source

repo-scoped Codex discovery
$REPO_ROOT/.agents/skills/<skill-name>
  → checked-in package or symlink when the Skill should be discoverable only there

external reusable distribution
OpenAI plugin or another explicit distribution artifact
```

OpenAI's current Codex discovery locations and symlink support are external platform
facts, not conventions invented by this repository. See
`references/skill-repository-policy.md` for the maintained-source/discovery contract.

Do not treat `/Users/wenv/Documents/skills/` itself as an automatic Codex discovery
location. Do not use legacy `~/.codex/skills/` as the canonical current discovery
contract.

## Scope boundaries

This repository owns global collaboration rules and reusable templates. It does not
own another project's scientific truth, tasks, Codex reports, workspaces, data,
experiments, manuscript, or project-specific concepts.

Project-specific assets remain in the repository that owns them.

## Maintenance rules

- User + ChatGPT own collaboration-system design; Codex executes committed local
  tasks that genuinely require local capabilities.
- Change the single owning `references/*` file for a collaboration operational rule;
  route to it instead of copying the rule into multiple files.
- Change root `SKILL.md` only when activation or top-level routing changes.
- Change root `AGENTS.md` only for repository-maintenance instructions or authority
  routing.
- Record this repository's concept entries as decision history/rationale; do not copy
  full current collaboration policy there.
- In project templates, preserve the distinction between canonical design authority,
  operational projection, implementation, verification, and runtime artifacts.
- Preserve formal task and Codex report paths after issue. Do not calendar-archive or
  rewrite closed artifacts merely for directory tidiness.
- Keep optional architecture conditional on a real owner, artifact, and consumer.

## Runtime

This repository is documentation/policy oriented and owns no independent runtime by
default. Do not create `pyproject.toml`, scripts, environments, or dependencies
without a real executable consumer and explicit approval.

## Hard invariants

- `references/*` is this repository's current operational-policy layer.
- This repository's `reports/concept/*` is decision history/rationale.
- A project may explicitly declare selected concepts as canonical design authority;
  its Skills/references then act as operational projections and must not redefine the
  design.
- Project design authority and source-grounded scientific fact authority are separate.
- `SKILL.md` routes; it does not duplicate protocol details.
- Maintained Skill source, Codex discovery, and external distribution are separate
  boundaries.
- Standalone first-party Skill source repositories retain their root `AGENTS.md` for
  maintenance; embedded sub-Skills normally inherit the nearest parent instructions.
- Project workflow Skill paths are project-declared; do not assume `project/SKILL.md`.
- Formal task/report artifacts keep stable repository paths once issued.
- User + ChatGPT design; Codex executes approved local work.
