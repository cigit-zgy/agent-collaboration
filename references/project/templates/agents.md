# Project AGENTS.md template

Read `../../collaboration/agents.md` first. This template specializes that writing standard for a maintained scientific/software project.

````markdown
# <PROJECT_NAME> project context

## Identity

<What this project produces and the repository scope.>

## Authority

User + ChatGPT develop and adjudicate project design. The User retains final design acceptance/override authority and designated human decision checkpoints. ChatGPT acts as design partner, connected author/executor, conversation-handoff author, and acceptance reviewer. Codex executes approved LOCAL implementation/execution and supplies evidence; zero-human-coding is permitted.

```text
reports/concept/                  canonical accepted design, when declared
<workflow>/SKILL.md + references  operational projection
scripts/code/schemas              implementation
tests                             conformance verification
registered source/evidence        model-specific scientific fact authority
reports/handoff/                  conversation continuity/context only; not authority
```

## Repository ownership

```text
<path>  <responsibility>
```

List only ownership boundaries that affect Agent behavior.

## Workflow

Project workflow Skill: `<PROJECT-DECLARED-SKILL-PATH>`

Routine:

```text
AGENTS.md
→ workflow SKILL.md
→ owning sub-Skill
→ required reference/script
```

Context recovery after conversation/session migration, when `reports/handoff/README.md` exists:

```text
AGENTS.md
→ reports/handoff/README.md
→ current handoff only
→ re-resolve current project/collaboration authority and current repository state
→ continue through the relevant routine/design route
```

Do not preload all historical handoffs. Handoffs are context snapshots only and never override current concept/task/source authority.

New project / new core subsystem / major algorithm or architecture design:

```text
AGENTS.md
→ agent-collaboration references/project/prior-art.md
→ authoritative literature + linked/mature open-source precedents
→ reports/concept/README.md
→ governing concept
→ affected Skill/reference
→ implementation/tests
```

The prior-art gate is mandatory for substantial new design. Search both literature→code and GitHub/source→scientific provenance; record the reuse/adapt/reference/reject result in the governing concept before freeze.

Routine design/redesign/conformance that does not introduce a new major design concern:

```text
AGENTS.md
→ reports/concept/README.md
→ governing concept
→ affected Skill/reference
→ implementation/tests
```

Conversation migration itself follows `agent-collaboration:references/project/handoff.md`. ChatGPT creates the new handoff and updates `reports/handoff/README.md`; Codex is not the primary handoff author.

## Shared coding Skills

Global profile:
`cigit-zgy/agent-collaboration@<COLLABORATION_REVISION>:references/collaboration/shared-coding-skills.md`

Project-specific additions/overrides:
`<NONE OR PROJECT-OWNED REFERENCE WITH IMMUTABLE SKILL COORDINATES>`

ChatGPT and Codex must use the same applicable Skill revisions/modes for code authoring, review, local verification, and repair. A local discovery path alone is not authority. Project scientific/product/trust rules and project tooling take precedence over generic coding Skills.

## Runtime and verification

<Runtime/tooling authority and stable common commands, if any. Mechanical code style belongs here/tooling rather than in collaboration prose.>

ChatGPT authors code/tests it can correctly produce from repository/design/shared-Skill context. Cheap checks already supported by ChatGPT's connected environment may run online; environment-bound or time-consuming verification runs through Codex locally. Do not duplicate expensive checks without a distinct evidentiary reason.

## Human / trust checkpoints

<Only genuine project-specific decisions or trust transitions. Preserve the User's final decision authority where a human decision is required; do not require human code authorship or line-by-line review unless the project explicitly chooses that policy.>

## Hard invariants

<Short project-wide hard boundaries. Include the prior-art gate when this project creates or materially redesigns core capabilities. When conversation handoff artifacts exist, keep `reports/handoff/README.md` current and treat handoffs as context-only snapshots.>
````

A project `AGENTS.md` routes to `agent-collaboration` for global collaboration, prior-art/reuse policy, conversation handoff/context recovery, AI-assisted implementation, shared coding-Skill alignment, Git, and verification policy rather than copying those manuals.
