---
id: 03
title: Project Integration and Collaboration Asset Lifecycle
status: active
created: 2026-09-02
updated: 2026-09-02
authority: global
scope: project AGENTS entrypoint and template, project-owned collaboration assets, weekly report archives, and concept lifecycle
supersedes: null
related_tasks: []
---

# Project Integration and Collaboration Asset Lifecycle

## Current conclusion

Each project repository uses root `AGENTS.md` as its project-level entry point and
constitution. The file links the project to the canonical
`cigit-zgy/agent-collaboration` repository for ChatGPT and to
`/Users/wenv/Documents/skills/agent-collaboration/SKILL.md` for Codex, then routes
the project's own `SKILL.md`, concept index, report directories, scientific/product
authorities, and project-specific precedence.

New projects use the canonical reusable scaffold
`references/project-agents-template.md`. User + ChatGPT instantiate that template
after inspecting the actual repository and resolving project-specific purpose,
authority, ownership, trust, runtime, workflow, and human checkpoints. The template
is not copied blindly. Project-constitution design remains a User + ChatGPT
responsibility; Codex may verify local discovery after the committed design exists,
but it does not design the constitution.

`agent-collaboration` owns only the shared collaboration protocol and reusable
onboarding templates. Project-specific ChatGPT tasks, Codex reports, and concept
conclusions remain in the project that owns them.

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

project/SKILL.md
= project workflow/router

project/reports/concept/
= durable User + ChatGPT conclusions

project/reports/chatgpt/
= implementation-ready Codex tasks

project/reports/codex/
= Codex execution evidence
```

ChatGPT enters a new project by reading the project's `AGENTS.md`, following its
canonical collaboration reference, reading only relevant concept topics from the
project concept index, and then reading the project Skill/router as needed. Codex
enters through machine-wide `~/.codex/AGENTS.md`, then the local collaboration Skill,
then the target project's `AGENTS.md` and project routing.

When a new repository lacks a suitable `AGENTS.md`, the onboarding path is:

```text
User identifies project
→ ChatGPT reads agent-collaboration
→ ChatGPT reads references/project-agents-template.md
→ ChatGPT inspects the repository
→ User + ChatGPT settle project-specific constitution decisions
→ ChatGPT writes/commits AGENTS.md when its connected tools are sufficient
→ Codex verifies local discovery only when that local verification is actually needed
```

The canonical template defines the stable project-entry categories without imposing
project-specific content: project identity, scope/precedence, project boundaries,
authority/trust, repository ownership, knowledge/report routing, workflow routing,
runtime/environment, human checkpoints, and a short list of project invariants.
Detailed global Git/verification procedure and detailed sub-Skill implementation do
not belong in project `AGENTS.md`.

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
expose the project constitution, design conclusions, execution specifications, and
execution evidence without searching a separate central report repository. The
global collaboration Skill should remain a reusable protocol rather than accumulating
project-specific history.

A canonical `AGENTS.md` scaffold prevents every new project from reinventing its
entry structure while still requiring User + ChatGPT to make the actual
project-specific design decisions. Keeping Codex out of constitution design preserves
the established design/execution authority split.

Independent weekly archives keep active report directories small while preserving
clear authorship boundaries. Topic-based concepts provide stable retrieval and avoid
forcing Agents to reconstruct current design truth from chronological logs.

#### Boundary

This concept governs project integration, the reusable project-entry scaffold, and
collaboration-asset lifecycle. It does not dictate project-specific scientific
content, project directory architecture outside collaboration assets, or a mandatory
weekly archive when no eligible files exist.

#### Impact

- project root `AGENTS.md`
- `references/project-agents-template.md`
- `references/project-integration.md`
- `references/report-concept-policy.md`
- project `reports/chatgpt/`, `reports/codex/`, and `reports/concept/`
- future project onboarding into the collaboration workflow

#### Related tasks

None. The decision was applied directly by ChatGPT through connected repository
tooling because it did not require local-machine execution.
