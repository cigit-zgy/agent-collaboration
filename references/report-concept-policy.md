# Report and concept asset policy

This file is the current operational authority for collaboration reports and project
concept assets.

## Stable report layout

```text
reports/
├── chatgpt/   committed local-execution specifications
├── codex/     execution and verification evidence
└── concept/   accepted project design specifications
```

Formal task/report paths are stable after issue. Do not calendar-archive, relocate, or
rewrite them merely for tidiness.

## Concept means accepted design only

For maintained research/scientific projects, `reports/concept/` contains only the
current User + ChatGPT accepted project solution/design.

A concept topic may define:

- project purpose and scientific positioning;
- architecture and stage boundaries;
- scientific representation design;
- interfaces and ownership;
- trust states and lifecycle;
- provenance/evidence design;
- validation/promotion design;
- human-review design;
- project-specific testing/release design.

A concept topic must not contain:

- chat transcript or discussion chronology;
- implementation progress/status;
- Codex execution evidence;
- test logs/results;
- temporary hypotheses;
- current filesystem/worktree state;
- code details that do not belong to the accepted design;
- model-specific scientific values copied from runtime/source artifacts.

Git history and `reports/chatgpt/` / `reports/codex/` preserve implementation and
change history. `reports/concept/` is not a history log.

## Single design authority

For a project that declares concept authority:

```text
Level 1  reports/concept/
         canonical accepted project solution/design

Level 2  SKILL.md + references/
         operational projection used by Agents

Level 3  scripts / source code / schemas
         implementation

Level 4  tests/
         conformance verification

Level 5  workspace/data/runtime artifacts
         produced or mutable project state
```

Levels 2–5 must conform to Level 1.

If a concept says `A`, a Skill/reference says `B`, and code implements `C`, the default
interpretation is that `B/C` drifted from the accepted design. Do not rewrite the
concept merely to match current implementation.

A design change occurs only when User + ChatGPT explicitly agree on a new solution and
update the governing concept first. Downstream projections, implementation, and tests
are then updated to realize that solution.

## Concept index

`reports/concept/README.md` is the design map. It identifies the accepted concept topics
and the downstream files that implement/project each topic.

Recommended fields:

```markdown
| ID | File | Design topic | Status | Operational projection |
|---|---|---|---|---|
```

The index is not an implementation-status board.

## Concept topic form

Keep metadata minimal:

```yaml
---
id: 03
title: User workspace architecture
status: active
role: design_authority
operational_projection:
  - <path/to/owning/SKILL-or-reference>
---
```

The body contains the current accepted solution only:

```markdown
# <Design topic>

## Accepted design

<Complete current solution for this topic.>
```

Do not add chronological `Decision history`, task logs, implementation notes, or test
results to the concept body. Historical evolution belongs to Git history and formal
reports.

## Runtime versus design work

Routine execution may use the already-derived operational projection:

```text
AGENTS.md
→ workflow SKILL.md
→ owning sub-Skill
→ required reference/script
```

But design, redesign, architecture review, implementation audit, or suspected drift
must begin from the governing concept:

```text
AGENTS.md
→ reports/concept/README.md
→ relevant concept design topic(s)
→ affected Skill/reference projection
→ implementation/tests as needed
```

This keeps routine Agent context small without weakening the concept as the unique
design source.

## Scientific source authority is separate

Project design truth and model scientific fact truth are different authorities:

```text
project design truth
= reports/concept/

model/source scientific facts
= registered original source + evidence/provenance chain
```

Concepts define how the system should represent, validate, and operate on scientific
facts. They do not invent model-specific values, equations, symbols, or claims.

## Collaboration repository exception

`agent-collaboration` itself is a protocol/Skill repository rather than a scientific
project. Its active operational rules remain in `references/*`. Its existing concept
files may remain historical design records, but project templates and project policy
must use the solution-only concept model above for maintained scientific/research
projects.

## Report metadata

New ChatGPT tasks and Codex reports use compact YAML identity/provenance metadata as
defined by `chatgpt-task-template.md` and `codex-report-template.md`. Do not repeat the
same identity block in the body or store self-referential containing-commit SHAs.
