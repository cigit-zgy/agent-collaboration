# Skill concept-first development and design-probing tests

## Decision

Maintained first-party Skills follow this authority order:

```text
accepted Skill/project concept or design authority
→ SKILL.md + references/
→ implementation
→ tests/evaluation
```

When a Skill task exposes a design problem, User + ChatGPT resolve and make the design durable first, then project it into Skill Markdown before code changes. Codex implements the committed Markdown contract and does not invent task-specific semantics in code.

## Testing purpose

Skill testing primarily probes whether the design and operational contract are sufficient, coherent, general, and implementable.

A test failure is classified before code repair as one of:

```text
DESIGN_GAP
PROJECTION_DRIFT
IMPLEMENTATION_DRIFT
TEST_DEFECT
ENVIRONMENT / TOOL DEFECT
```

A triggering task becoming green is not enough if the implementation depends on fixture-specific branches or the durable contract remains ambiguous.

## Pure implementation exception

If the concept and Skill Markdown already determine the correct behavior without interpretation, code may be repaired directly as implementation drift. Concept files are not edited merely for ceremony.

## Rationale

Task-driven patching tends to accumulate narrow fixes that optimize one current example while weakening the reusable Skill abstraction. Concept-first projection keeps semantics at durable owners and lets tests expose flaws in the design itself rather than train the implementation toward one task.

## Operational owner

```text
references/skill/development.md
```

Supporting routing/templates may summarize this rule, but the detailed lifecycle has one owner there.
