---
id: 03
title: Project Integration and Collaboration Asset Lifecycle
status: active
created: 2026-09-02
updated: 2026-09-02
authority: global
scope: project AGENTS/workflow-Skill entry templates, project-owned collaboration assets, weekly report archives, and concept lifecycle
supersedes: null
related_tasks: []
---

# Project Integration and Collaboration Asset Lifecycle

## Current conclusion

Each maintained project repository uses root `AGENTS.md` as its project-level entry
point and constitution. The file links the project to canonical
`cigit-zgy/agent-collaboration`, routes the project concept/report locations, and
declares the canonical Agent-facing project workflow Skill when one exists.

The project workflow Skill does not need to live at repository root. For coordinated
multi-Skill Agent projects, the preferred pattern is a project-specific Agent package:

```text
<project>/
├── AGENTS.md
└── <agent-name>/
    ├── SKILL.md
    ├── <capability-a>/SKILL.md
    └── <capability-b>/SKILL.md
```

Root `AGENTS.md` declares the actual workflow path. Do not create a duplicate root
`SKILL.md` merely for symmetry.

Water-domain project onboarding uses three reusable authorities:

```text
references/project-architecture.md
→ repository responsibility map and required/conditional paths

references/project-agents-template.md
→ project constitution and repository routing

references/project-skill-template.md
→ Agent-facing project workflow/router, when such a workflow exists
```

User + ChatGPT instantiate these after inspecting the actual repository and deciding
project-specific purpose, authority, ownership, trust, runtime, workflow, stage
boundaries, and human checkpoints. Codex may verify committed local discovery/runtime
behavior but does not design the constitution or silently redefine workflow semantics.

A project workflow `SKILL.md` follows progressive disclosure. For each top-level
stage/capability, the preferred routing description is limited to five facts:

```text
purpose
required input
stable output
next-stage gate
owning Skill
```

`agent-collaboration` owns only shared collaboration rules and reusable architecture /
template authorities. Project-specific tasks, reports, concepts, constitutions,
Agent packages, Skills, scientific assets, and workspaces remain in the owning
project repository.

Closed ChatGPT and Codex report pairs are organized about weekly by moving them with
Git into independent archives:

```text
reports/chatgpt/archive/<MONDAY_YYMMDD>/
reports/codex/archive/<MONDAY_YYMMDD>/
```

Only fully closed and independently audited task pairs are eligible. Active work
remains at the root of its report directory. Archive means move, not duplicate.

Concept assets are not archived weekly. They are organized by durable topic. Each
concept exposes an authoritative `Current conclusion` plus concise chronological
`Decision history`. A calendar week alone does not create a concept checkpoint.

## Decision history

### 2026-09-02

#### Conclusion

The standard project relationship was established as:

```text
agent-collaboration
= global collaboration rules + reusable project-entry templates

project/AGENTS.md
= project entry point and constitution

project workflow SKILL.md
= Agent-facing project workflow/router

project downstream Skills
= detailed bounded capability procedures

project/reports/concept/
= durable User + ChatGPT conclusions

project/reports/chatgpt/
= implementation-ready Codex tasks

project/reports/codex/
= Codex execution evidence
```

Project onboarding, report ownership, weekly report archives, and topic-based concept
lifecycle were established. User + ChatGPT own constitution/workflow design; Codex
executes committed local tasks.

#### Rationale

A project should remain self-contained and should expose governance, workflow,
durable design truth, execution specifications, and execution evidence without moving
project truth into a global collaboration repository.

#### Boundary

This concept governs project integration and collaboration-asset lifecycle, not the
scientific contents of a specific project.

#### Impact

- project `AGENTS.md`
- project workflow `SKILL.md`
- project collaboration reports/concepts
- project onboarding

#### Related tasks

None.

### 2026-09-02 — workflow-location refinement

#### Conclusion

The earlier phrase “project root `SKILL.md`” was too restrictive. The canonical rule
is now:

> root `AGENTS.md` is the repository entry; the Agent-facing workflow `SKILL.md`
> lives at the one project-declared canonical path.

For multi-Skill Agent projects, `<agent-name>/SKILL.md` is preferred because the
coordinated sub-Skills form the Agent capability system. A repository-root
`SKILL.md` remains valid only when it is genuinely the canonical workflow location.

Project architecture itself is now governed separately by
`references/project-architecture.md` and concept 05.

#### Changes from previous conclusion

- removed the assumption that project workflow Skill must be repository-root;
- added explicit `<agent-name>/SKILL.md` multi-Skill Agent pattern;
- separated project responsibility architecture from collaboration integration;
- retained root `AGENTS.md` as the universal maintained-project entry.

#### Rationale

This matches actual projects such as `water-biomodel-agent`, where repository-level
governance applies to more than the Agent software package, while the coordinated
Skills belong inside the Agent package itself.

#### Boundary

This refinement changes Skill placement/routing semantics only. It does not change
report lifecycle, concept lifecycle, or collaboration authority.

#### Impact

- `references/project-integration.md`
- `references/project-agents-template.md`
- `references/project-skill-template.md`
- root collaboration `SKILL.md`
- future project onboarding

#### Related tasks

None.
