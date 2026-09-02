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

## Design authority

<DECLARE THE PROJECT'S DESIGN-AUTHORITY MODEL.>

For a maintained scientific/research project whose accepted User + ChatGPT plans are
stored as canonical concepts, use:

```text
reports/concept/
= canonical project design specification for declared topics

workflow/sub-Skills + references/
= operational projection of that design

scripts/code/schemas
= implementation

tests/
= conformance verification
```

Downstream projections and implementation must conform to governing design-authority
concepts. If they disagree, treat the difference as implementation/projection drift;
do not silently rewrite the concept to match current code.

A design change is accepted only when User + ChatGPT explicitly update the governing
concept first, then update its operational projections and implementation.

If this project uses concepts only as history/rationale instead, state that explicitly
and point to the current operational authority.

Model/source scientific facts remain separate from project design authority. State
the project's scientific evidence/provenance authority when relevant.

## Authority and trust

<STATE THE PROJECT'S SOURCE-OF-TRUTH / TRUST ORDER.>

Example:

```text
registered source evidence
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

For design/redesign/conformance-audit work in a project with design-authority
concepts:

```text
AGENTS.md
→ reports/concept/README.md
→ relevant design-authority concept(s)
→ affected SKILL/reference projection
→ implementation/tests as needed
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
reports/concept/   role declared above: design authority or decision history/rationale
```

Do not force concept loading into ordinary runtime merely because concepts are design
authority. Runtime uses their current operational projections; design/audit tasks read
the governing concept directly.

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
→ User + ChatGPT settle purpose/authority/ownership/design-authority model
→ ChatGPT instantiates this AGENTS.md
→ bootstrap only the minimum assets defined by project-architecture.md
→ record canonical project design before projecting it into Skills/references when applicable
→ add a project workflow Skill only when a real Agent-operable workflow exists
→ Codex verifies local discovery/runtime or implements frozen design only when genuinely needed
```

Do not delegate project-constitution or scientific/architectural design to Codex merely
because Codex can edit files locally.

## Quality criteria

A good project `AGENTS.md` answers quickly:

1. What is this project?
2. What is the canonical project design authority?
3. What separate source-evidence authority applies to scientific facts, if relevant?
4. What project-local trust model applies?
5. Who owns which repository responsibility?
6. What workflow Skill, if any, should be read next?
7. What runtime authority applies?
8. Which decisions require a human?
9. When must an Agent read a governing concept rather than only its operational projection?

Detailed implementation, test commands, sub-Skill internals, and global Git/
verification procedure belong elsewhere.
