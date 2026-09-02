---
id: 03
title: Project Integration and Collaboration Asset Lifecycle
status: active
created: 2026-09-02
updated: 2026-09-02
authority: global
scope: project AGENTS/SKILL entry templates, project-owned collaboration assets, weekly report archives, and concept lifecycle
supersedes: null
related_tasks: []
---

# Project Integration and Collaboration Asset Lifecycle

## Current conclusion

Each project repository uses root `AGENTS.md` as its project-level entry point and
constitution. The file links the project to the canonical
`cigit-zgy/agent-collaboration` repository for ChatGPT and to
`/Users/wenv/Documents/skills/agent-collaboration/SKILL.md` for Codex, then routes
the project's own root `SKILL.md`, concept index, report directories,
scientific/product authorities, and project-specific precedence.

New projects use two canonical reusable scaffolds in order:

```text
references/project-agents-template.md
→ project constitution and project-level routing

references/project-skill-template.md
→ Agent-facing project workflow/router
```

User + ChatGPT instantiate these templates after inspecting the actual repository and
resolving project-specific purpose, authority, ownership, trust, runtime, workflow,
stage boundaries, and human checkpoints. The templates are not copied blindly.
Project-entry and workflow design remain User + ChatGPT responsibilities; Codex may
verify committed local discovery/runtime behavior, but it does not design the
constitution or silently redefine workflow semantics.

A project root `SKILL.md` follows progressive disclosure. It should be compact enough
for an unfamiliar compatible Agent to understand when the workflow applies, what
entry state is required, what the canonical top-level stages are, what each stage
consumes and produces, which gate permits progression, which downstream Skill owns
the detailed procedure, and when execution must stop. For each top-level stage the
preferred root-level description is limited to five routing facts: purpose, required
input, stable output, next-stage gate, and owning Skill.

`agent-collaboration` owns only the shared collaboration protocol and reusable
onboarding templates. Project-specific ChatGPT tasks, Codex reports, concept
conclusions, project constitutions, and project Skills remain in the project that owns
them.

Closed ChatGPT and Codex report pairs are organized about weekly by moving them with
Git into independent archives:

```text
reports/chatgpt/archive/<MONDAY_YYMMDD>/
reports/codex/archive/<MONDAY_YYMMDD>/
```

The files are moved, not copied. Only fully closed and independently audited task
pairs are eligible. Active work remains at the root of its respective report
directory. Archive folders use the Monday of the completion week.

Concept assets are not archived weekly. They are organized by durable topic. Each
new concept file contains a concise authoritative `Current conclusion` plus a
chronological `Decision history`. User + ChatGPT add a history checkpoint only when
a mature stage conclusion materially changes durable project truth; a calendar week
alone does not create a concept entry.

## Decision history

### 2026-09-02

#### Conclusion

The standard project relationship is:

```text
agent-collaboration
= global collaboration rules + reusable project-entry templates

project/AGENTS.md
= project entry point and constitution

project/root SKILL.md
= Agent-facing project workflow/router

project/downstream Skills
= detailed stage procedures and references

project/reports/concept/
= durable User + ChatGPT conclusions

project/reports/chatgpt/
= implementation-ready Codex tasks

project/reports/codex/
= Codex execution evidence
```

ChatGPT enters a project by reading its `AGENTS.md`, following the canonical
collaboration reference, reading only relevant concept topics from the project
concept index, and then reading the root project Skill and owning downstream Skill as
needed. Codex enters through machine-wide `~/.codex/AGENTS.md`, then the local
collaboration Skill, then the target project's `AGENTS.md` and project routing.

When a new repository lacks suitable project entry assets, the onboarding path is:

```text
User identifies project
→ ChatGPT reads agent-collaboration
→ ChatGPT reads references/project-agents-template.md
→ ChatGPT inspects the repository
→ User + ChatGPT settle project constitution decisions
→ ChatGPT writes/commits AGENTS.md when connected tools are sufficient
→ ChatGPT reads references/project-skill-template.md
→ User + ChatGPT settle canonical workflow and stage boundaries
→ ChatGPT writes/commits root SKILL.md when connected tools are sufficient
→ Codex verifies local discovery/runtime only when that local verification is actually needed
```

The `AGENTS.md` template defines the stable project-entry categories without
imposing project-specific content: project identity, scope/precedence, project
boundaries, authority/trust, repository ownership, knowledge/report routing,
workflow routing, runtime/environment, human checkpoints, and a short list of project
invariants.

The root `SKILL.md` template follows the public Agent Skills style: YAML `name` and a
trigger-oriented `description`, then a compact workflow router. It separates
activation, inputs, canonical stages, stage routing, optional trust/lifecycle
progression, progressive disclosure, runtime entry, stop conditions, and boundaries.
Detailed schemas, algorithms, scientific rules, repair logic, and command sequences
belong in downstream Skills/references rather than the root router.

Report archives are local to each report owner rather than centralized under one
`reports/archive/` tree:

```text
reports/chatgpt/archive/260831/
reports/codex/archive/260831/
```

The weekly folder name is the Monday beginning the completion week, formatted as
`YYMMDD`. `git mv` preserves one active truth rather than creating duplicate copies.
Any repository-relative metadata links are updated when files move.

Concepts use stable topic files rather than weekly files. `Current conclusion` is
the current authority; `Decision history` preserves the accepted stages and why the
current conclusion evolved.

#### Rationale

A project should remain self-contained: cloning or inspecting its repository should
expose the project constitution, workflow router, design conclusions, execution
specifications, and execution evidence without searching a separate central report
repository. The global collaboration Skill should remain a reusable protocol rather
than accumulating project-specific history.

Canonical `AGENTS.md` and root `SKILL.md` scaffolds prevent every new project from
reinventing its entry structure while still requiring User + ChatGPT to make the
actual project-specific design decisions. Keeping Codex out of constitution and
workflow design preserves the established design/execution authority split.

Independent weekly archives keep active report directories small while preserving
clear authorship boundaries. Topic-based concepts provide stable retrieval and avoid
forcing Agents to reconstruct current design truth from chronological logs.

#### Boundary

This concept governs project integration, reusable project-entry/workflow scaffolds,
and collaboration-asset lifecycle. It does not dictate project-specific scientific
content, project directory architecture outside collaboration assets, or a mandatory
weekly archive when no eligible files exist.

#### Impact

- project root `AGENTS.md`
- project root `SKILL.md`
- `references/project-agents-template.md`
- `references/project-skill-template.md`
- `references/project-integration.md`
- `references/report-concept-policy.md`
- project `reports/chatgpt/`, `reports/codex/`, and `reports/concept/`
- future project onboarding into the collaboration workflow

#### Related tasks

None. The decision was applied directly by ChatGPT through connected repository
tooling because it did not require local-machine execution.
