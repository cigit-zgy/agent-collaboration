# Maintained Skill-repository AGENTS.md template

Read `../../collaboration/agents.md` first. Use this specialization for a standalone maintained first-party Skill source repository.

````markdown
# <SKILL_NAME> repository context

## Identity

This repository is the maintained first-party source for the `<SKILL_NAME>` Skill.

<One concise capability/repository description.>

## Authority

```text
<governing concept/design authority>  accepted Skill semantics, when declared
SKILL.md                              Agent-facing trigger/workflow/router
references/                           bounded specialized Skill contracts
scripts/code/schema                   implementation
Tests/evaluation                      design/conformance evidence
```

User + ChatGPT maintain Skill design. The User retains final decision/override authority and designated human checkpoints. ChatGPT performs connected DIRECT design/Markdown/code/test authoring and acceptance review. Codex executes approved LOCAL implementation/verification/repair and does not self-accept.

## Collaboration entry

Global collaboration authority:
`cigit-zgy/agent-collaboration@<COLLABORATION_REVISION>`

Runtime collaboration entry:
`SKILL.md`

Do not preload the collaboration repository. Resolve the maintenance concern through its direct routing table.

Skill behavior/design/testing lifecycle:
`references/skill/development.md`

Skill Markdown/reference writing:
`references/skill/writing.md`

Maintained source/discovery/distribution:
`references/skill/repository.md`

Package/resources/runtime ownership:
`references/skill/package.md`

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

## Development workflow

Design-bearing changes:

```text
accepted concept/design
→ SKILL.md + owning references
→ implementation
→ design-probing tests
```

If tests expose a capability/workflow/routing/trust/recovery/completion design gap, return to concept/design and Skill Markdown before implementation repair.

Pure implementation drift may be repaired directly only when the durable concept/Skill contract already determines expected behavior without interpretation.

## Progressive disclosure

The maintained Skill should route directly from `SKILL.md` to the relevant specialized owner. Avoid mandatory second indexes and reference chains.

Templates/examples/history remain cold unless the active branch needs them.

## Runtime and verification

<No independent runtime | runtime authority + mechanical style/verification route.>

## Hard invariants

- Skill semantics are not invented only in code/tests/task prose.
- `SKILL.md` is the capability runtime entry/router.
- References have bounded owners and are loaded on demand.
- <Additional repository-specific source/discovery/ownership boundaries.>
````

Embedded sub-Skills normally inherit the nearest project `AGENTS.md`; a separate local file is justified only by real subtree-specific maintenance rules.
