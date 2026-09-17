# Project living-Design authoring template

Cold path: load only when creating/restructuring `reports/design/`.

Current-Design semantics are owned by `../design.md`; backstop maintenance by `../reconciliation.md`.

## Directory shape

Default mature shape:

```text
reports/design/
├── README.md
├── 00_overview.md
├── 01_domain_and_objects.md
├── 02_workflow_and_state.md
├── 03_artifacts_and_ownership.md
├── 04_interfaces.md
├── 05_trust_and_validation.md
└── 06_runtime_and_skills.md
```

These semantic slots are defaults, not mandatory filenames. Omit or merge responsibilities that do not exist.

Healthy default: roughly 5–8 current topics. Before adding topic 9+, inspect consolidation. Above 12, do not add another topic by default without User approval or a clearly independent responsibility.

## README.md

Keep it navigational plus compact reconciliation metadata:

```yaml
---
design_reconciliation:
  enabled: true
  reconciled_at: YYYY-MM-DD
  chatgpt_through: YYMMDD_chatgpt_NN | null
  codex_through: YYMMDD_codex_NN | null
  concept_through: YYMMDD_concept_NN | null
---
```

Use `enabled: true` only when this repository should participate in periodic ChatGPT Design reconciliation.

Then map each current topic once:

```markdown
# Design map

| Order | design_id | File | Responsibility |
|---:|---|---|---|
| 00 | overview | `00_overview.md` | Whole-system architecture |
| 01 | <id> | `01_<topic>.md` | <one sentence> |
```

Do not restate topic semantics or progress history in README.

## Topic file

```markdown
---
design_id: <stable-semantic-id>
title: <title>
status: active
role: design_authority
summary: >
  <one-sentence owned concern>
operational_projection:
  - <real downstream path when useful>
---

# <Title>

## Purpose
## Boundary
## Accepted design
## Invariants / trust boundaries
## Ownership and interfaces
## Design acceptance
```

Remove empty sections rather than adding ceremony.

## One-owner check

A bounded concern routes to one primary topic plus at most one necessary secondary topic. If one rule needs three or more current topics, restructure ownership before adding another topic.

Do not keep a current topic whose main role is to supersede, refine, override, or preserve another current topic for the same concern.

When responsibility changes:

```text
update/overwrite the real owner
→ merge/split/remove/reorder as needed
→ update README.md
→ remove superseded current files
```

Git preserves prior Design states. Reports preserve work/evidence history.

## Runtime and Skill profile

When multiple reusable Skills matter, keep one current Design owner for:

```text
Skill/tool
immutable authority/source when applicable
activation condition
required | conditional
purpose
```

Do not copy Skill manuals into Design.

## Content check

Reject content whose primary owner is:

```text
source/model-specific scientific fact
test/evaluation output
ChatGPT/Codex task or execution history
current status/backlog
chronological discussion
```

Keep only current project Design semantics with a real reusable owner.
