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

User + ChatGPT own project design. Codex executes approved committed local tasks and
must not silently redesign the accepted solution.

## Design authority

For maintained scientific/research projects:

```text
reports/concept/
= canonical accepted project solution/design

workflow/sub-Skills + references/
= operational projection of that solution

scripts/code/schemas
= implementation

tests/
= conformance verification
```

Concept files contain the accepted solution only. Do not place chat chronology,
implementation status, task history, test results, or runtime state in concept files.

If downstream projection or implementation disagrees with the governing concept,
treat the difference as drift. Do not rewrite the concept to match current code.
A design change requires an explicit User + ChatGPT decision and concept update first.

Model/source scientific facts remain separate from project design authority and are
grounded in the project's registered source/evidence chain.

## Authority and trust

<STATE THE PROJECT'S SOURCE-OF-TRUTH / TRUST ORDER.>

Example:

```text
registered source evidence
→ derived representation
→ machine-validated state
→ human-approved state
```

## Repository ownership

```text
<path>/    <responsibility>
<path>/    <responsibility>
```

List only boundaries that affect Agent behavior. State immutable/read-only areas
explicitly.

## Workflow routing

Project workflow Skill: `<PROJECT-DECLARED-SKILL-PATH>`

Routine execution:

```text
AGENTS.md
→ declared workflow SKILL.md
→ owning sub-Skill
→ required reference/script
```

Design/redesign/conformance audit:

```text
AGENTS.md
→ reports/concept/README.md
→ relevant concept topic(s)
→ affected SKILL/reference
→ implementation/tests as needed
```

## Runtime and environment

<STATE THE PROJECT RUNTIME AUTHORITY OR "No project runtime".>

## Collaboration assets

```text
reports/concept/   accepted project solution/design only
reports/chatgpt/   committed local-execution tasks
reports/codex/     Codex execution evidence
```

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
→ ChatGPT inspects repository
→ User + ChatGPT define accepted solution in reports/concept/
→ ChatGPT instantiates/normalizes project AGENTS.md
→ project Skills/references project that solution into operation
→ implementation follows the projection
→ tests verify conformity
→ Codex is used only for genuinely local execution/verification
```

Do not delegate project design to Codex merely because Codex can edit local files.

## Quality criteria

A good project `AGENTS.md` answers quickly:

1. What is this project?
2. Where is the canonical accepted design?
3. What separate scientific source authority applies?
4. What trust model applies?
5. What workflow Skill should be read next?
6. Which runtime authority applies?
7. When must the governing concept be read directly?
