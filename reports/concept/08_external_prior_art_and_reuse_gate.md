---
id: 08
title: External prior-art and reuse gate decisions
status: active
created: 2026-09-04
updated: 2026-09-04
role: decision_history
operational_authority:
  - references/project/prior-art.md
  - references/project/concept.md
  - references/project/architecture.md
  - references/collaboration/implementation.md
related_tasks: []
---

# External prior-art and reuse gate decisions

## Decision record

### 2026-09-04 — Search authoritative external precedent before substantial custom design

- Decision: new maintained projects, new core subsystems, major algorithm/architecture changes, important trust/provenance mechanisms, and substantial framework/tool choices must complete an external prior-art gate before concept freeze or substantial custom implementation.
- Required search directions: authoritative literature → linked/open implementation, and GitHub/source implementation → scientific/institutional provenance.
- Priority: paper-linked author/official repositories, official scientific/standards projects, and mature maintained open source with traceable scientific provenance are preferred over ungrounded custom design.
- Domain emphasis: for relevant water/environmental/scientific-computing work, the search explicitly includes high-level venues such as the Nature portfolio, Water Research, Environmental Science & Technology, and other field-leading journals relevant to the actual method.
- Concept consequence: gate-triggered concepts record a compact prior-art basis and classify serious candidates as `REUSE`, `ADAPT`, `REFERENCE_ONLY`, or `REJECT`; custom design must identify the concrete remaining gap.
- Boundary: external prior art is evidence, not project authority. User + ChatGPT retain project design authority, and scientific/product/trust requirements are not weakened to match an external project.
- Rationale: reduce wheel reinvention, improve scientific and engineering quality, and make concept formation evidence-first rather than internally speculative.
- Operational authority: `references/project/prior-art.md`, with freeze lifecycle in `references/project/concept.md` and implementation enforcement in `references/collaboration/implementation.md`.
