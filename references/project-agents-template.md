# Project `AGENTS.md` template

Use this scaffold for a maintained project repository. Root `AGENTS.md` is the
project-local constitution and Codex instruction entry. Keep it concise and durable.
Do not copy global collaboration mechanics or downstream workflow manuals into it.

```markdown
# <PROJECT_NAME> project context

## Project identity

<ONE-TO-THREE SENTENCES: what the project is, what it produces, and why it exists.>

## Collaboration and precedence

Canonical collaboration repository:
`cigit-zgy/agent-collaboration`

Codex local collaboration source:
`/Users/wenv/Documents/skills/agent-collaboration/SKILL.md`

Project-specific scientific, product, architectural, safety, and trust rules in this
repository are more specific for this project. User + ChatGPT own design; Codex
executes approved committed local tasks.

## Authority and trust

<STATE THE PROJECT'S SOURCE-OF-TRUTH / TRUST ORDER.>

Example:

```text
source evidence
→ derived representation
→ machine-validated state
→ human-approved state
```

Do not invent trust states when the project has none.

## Repository ownership

```text
<path>/    <responsibility>
<path>/    <responsibility>
```

List only boundaries that affect Agent behavior. State immutable/read-only areas
explicitly.

## Workflow routing

Project workflow Skill: `<PROJECT-DECLARED-SKILL-PATH>`

If no Agent-operable workflow exists, say so rather than creating a placeholder
Skill.

For normal runtime work:

```text
AGENTS.md
→ declared workflow SKILL.md
→ owning sub-Skill
→ only resources required by that route
```

## Runtime and environment

<STATE THE PROJECT RUNTIME AUTHORITY OR "No project runtime".>

Example:

```text
Environment: <ENVIRONMENT_NAME>
Dependency/tooling authority: <pyproject.toml | other contract>
```

## Collaboration assets

When they exist:

```text
reports/chatgpt/   committed local-execution tasks
reports/codex/     Codex execution evidence
reports/concept/   decision history/rationale
```

Concepts are not current operational policy and are not part of normal runtime
loading. Read `reports/concept/README.md` only when design history, rationale, or
supersession is materially needed.

## Human checkpoints

<LIST ONLY PROJECT-SPECIFIC HUMAN DECISIONS.>

## Hard project invariants

- <INVARIANT 1>
- <INVARIANT 2>
- <INVARIANT 3>
```

## Onboarding procedure

```text
User identifies project
→ ChatGPT reads project-architecture.md
→ ChatGPT inspects actual repository
→ User + ChatGPT settle purpose/authority/ownership
→ ChatGPT instantiates this AGENTS.md
→ bootstrap only the minimum assets defined by project-architecture.md
→ add a project workflow Skill only when a real Agent-operable workflow exists
→ Codex verifies local discovery/runtime only when genuinely needed
```

Do not delegate project-constitution design to Codex merely because Codex can edit
files locally.

## Quality criteria

A good project `AGENTS.md` answers quickly:

1. What is this project?
2. What project-local authority/trust model applies?
3. Who owns which repository responsibility?
4. What workflow Skill, if any, should be read next?
5. What runtime authority applies?
6. Which decisions require a human?
7. Where is historical decision rationale if needed?

Detailed implementation, test commands, sub-Skill internals, and global Git/
verification procedure belong elsewhere.
