# Skill development lifecycle

Load this reference when changing maintained first-party Skill behavior, projection, implementation, or tests.

## Authority

```text
reports/design/ current accepted semantics
→ SKILL.md + references operational projection
→ scripts/code/schema/config implementation
→ tests/evaluation evidence
```

`reports/concept/` is historical only and is created only when the User explicitly asks to persist Concept material.

Code and tests do not independently define Skill behavior.

## Classify the change first

```text
DESIGN_GAP
= current Design does not determine the required behavior
→ User + ChatGPT adjudicate
→ update reports/design/
→ then update Skill projection

PROJECTION_DRIFT
= Design is clear; SKILL.md/references are stale or incomplete
→ repair Skill Markdown

IMPLEMENTATION_DRIFT
= Design + Skill Markdown are clear; code violates them
→ repair implementation

TEST_DEFECT
= test requires behavior not owned by current Design/Skill
→ repair/remove test

ENVIRONMENT_OR_TOOL_DEFECT
= failure belongs to runtime/external interface
→ repair at that owner
```

Do not convert a real `DESIGN_GAP` into an implementation patch merely to finish a task.

## Development behavior

Inside already accepted semantics, Agents may choose the implementation path and should follow through through repair/retest without asking for routine approval.

For a design-bearing change, make the accepted semantics durable in current Design and Skill Markdown before production implementation depends on them.

A task is an execution specification, not the sole owner of new Skill semantics.

## Generality

Do not add production behavior solely for one task, fixture, paper, repository, model, or sample unless that behavior belongs to the intended capability class.

A concrete failure may reveal a general missing rule. Fix that rule at the owning Design/Skill surface rather than accumulating special cases.

## Testing

Use representative evidence that challenges the general Skill contract. Prefer meaningful normal flows, boundary cases, cross-stage invariants, failure/recovery behavior, and real artifacts when domain reality matters.

Do not add tests mechanically for every implementation detail or every historical incident. Verification proportionality is owned by `../collaboration/verification.md`.

## Prior art

For a new Skill, major capability, or substantial redesign, apply `../project/prior-art.md` when that gate is triggered before accepting custom Design.

## Completion

Skill development is complete when the accepted semantics are represented once in current Design, Skill Markdown projects them clearly, implementation conforms without task-specific semantics, and the necessary evidence establishes the intended capability.
