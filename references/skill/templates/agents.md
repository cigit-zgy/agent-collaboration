# Maintained Skill-repository AGENTS.md template

Read `../../collaboration/agents.md` first. Use this specialization for a standalone maintained first-party Skill source repository.

````markdown
# <SKILL_NAME> repository context

## Identity

This repository is the maintained first-party source for the `<SKILL_NAME>` Skill.

<One concise capability/repository description.>

## Authority

```text
<governing reports/concept/... or other accepted design authority>  Skill design semantics
SKILL.md                                                        Agent-facing capability/workflow entry
references/                                                     Skill-specific operational contracts
scripts/code/schema                                             implementation
 tests/evaluation                                               conformance + design-probing evidence
reports/                                                        collaboration/history assets when this repository owns them
```

User + ChatGPT maintain Skill design. ChatGPT performs connected DIRECT design/Markdown/code work and acceptance review; the User retains final decision/override authority and designated human checkpoints. Codex executes approved LOCAL implementation/execution and does not invent unresolved Skill semantics. Zero-human-coding is permitted.

## Repository ownership

```text
SKILL.md        <responsibility>
references/     <if present>
scripts/        <if present>
assets/         <if present>
tests/          <if present>
pyproject.toml  <if present>
README.md       <if present>
```

List only real paths.

## Skill development lifecycle — hard boundary

Use `agent-collaboration/references/skill/development.md` as the owner of the Skill development lifecycle.

For a design-bearing change:

```text
governing concept/design
→ SKILL.md + references/
→ implementation
→ tests/evaluation
```

When a failing task/test exposes a design gap, update/adjudicate the governing concept first, then update Skill Markdown, then code. Do not patch production code merely to make the current task/example pass while the durable contract remains ambiguous.

Pure implementation drift may be repaired directly only when concept + Skill Markdown already determine the expected behavior without interpretation.

Testing primarily challenges whether the Skill design is sufficient, coherent, general, and implementable. Tests are not optimized around one task fixture. Classify failures as `DESIGN_GAP | PROJECTION_DRIFT | IMPLEMENTATION_DRIFT | TEST_DEFECT | ENVIRONMENT/TOOL_DEFECT` before changing code.

## Source / discovery / distribution

Use `agent-collaboration/references/skill/repository.md` as the owner of maintained-source location, Codex discovery exposure, and external distribution policy. State repository-local exceptions here only when this Skill genuinely differs from that policy.

## Workflow

Use `SKILL.md` for capability operation.

When maintaining the Skill itself, use:

```text
agent-collaboration/references/skill/development.md
→ concept-first development lifecycle

agent-collaboration/references/skill/writing.md
→ SKILL.md/reference writing quality

agent-collaboration/references/collaboration/implementation.md
→ AI-assisted code quality and engineering discipline

agent-collaboration/references/collaboration/verification.md
→ verification level/evidence/placement
```

## Runtime and verification

<No independent runtime | runtime authority + mechanical style/verification route.>

## Hard invariants

- New/changed Skill semantics live in the governing concept/design and operational Skill Markdown before implementation.
- FORMAL task prose is not the sole owner of Skill behavior.
- Codex does not introduce task-specific semantic branches absent from the Skill contract.
- Tests probe the general design and its boundaries; a green triggering fixture is insufficient evidence by itself.
- <Other real source/discovery/ownership boundaries specific to this repository.>
````

Embedded sub-Skills normally inherit the nearest project `AGENTS.md`; a separate local file is justified only by real subtree-specific maintenance rules.
