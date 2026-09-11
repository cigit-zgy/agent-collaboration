# External prior-art and reuse contract

This contract governs evidence search before substantial new project design or custom implementation.

## Purpose

Do not invent a project architecture, core algorithm, scientific workflow, or major infrastructure component before checking strong published/open-source precedents.

```text
search credible prior art
→ inspect strongest implementations/rationale
→ decide REUSE | ADAPT | REFERENCE_ONLY | REJECT
→ record exploration in reports/concept/ when useful
→ reduce accepted consequence into reports/design/
→ implement only the remaining project-specific gap
```

External prior art is evidence, not project authority. User + ChatGPT remain design decision-makers. Current accepted design lives in `reports/design/`.

## Trigger

Run this gate for a new maintained project/core subsystem/major algorithm or modeling method/major architecture redesign/new trust-provenance-state mechanism/substantial framework or dependency choice/custom capability likely to exist in mature open source.

Ordinary bug fixes, typo/docs edits, bounded refactors, and direct implementation of already accepted design do not require reopening the gate unless a genuine new design choice appears.

If the gate applies, do not accept the design into `reports/design/` or begin substantial custom implementation until the search/reuse decision is complete.

## Mandatory two-way search

Search both:

```text
literature → code
AND
GitHub/source → scientific or institutional provenance
```

For scientific/environmental work, prioritize directly relevant high-level venues such as the Nature portfolio, Water Research, ES&T and ES&T Letters when in scope, without treating venue prestige as automatic authority.

GitHub stars/forks/ranking are maintenance/community signals only.

## Source priority

Prefer, when relevance is comparable:

1. author/official code linked from peer-reviewed work;
2. scientific organization/standards/long-lived domain projects;
3. mature maintained OSS with traceable scientific provenance;
4. weaker-provenance repositories only as secondary engineering precedent.

## Candidate inspection

For serious candidates inspect enough to recover the actual design boundary: methods/supplement, Code Availability/DOI/release, docs, architecture, API/schema/config, core flow, representative tests/examples, maintenance/release state, license, and material limitations.

For each candidate determine:

```text
problem boundary
key objects/stages/interfaces
invariants/trust assumptions
reusable implementation
adaptable pattern
project mismatches
remaining local gap
```

## Disposition

```text
REUSE          adopt maintained dependency/tool/project
ADAPT          reuse proven architecture/bounded implementation with project-specific change
REFERENCE_ONLY use as design evidence only
REJECT         unsuitable; record decisive reason when otherwise strong
```

Prefer REUSE/ADAPT when they satisfy scientific/product/trust/licensing/runtime constraints.

## Recording and reduction

Detailed search/reasoning belongs in `reports/concept/` when material. Preserve provenance/version/license coordinates for reused code and stable citations/DOIs for papers shaping design.

After adjudication:

```text
reports/concept/ = search/reasoning/history
reports/design/  = accepted current semantics only
```

Do not copy rejected alternatives or chronological search narrative into living design.

## Refresh

Repeat the gate when a major concern is introduced/reopened, an important tool/dependency is replaced, or new evidence suggests a substantially better established solution. Do not repeat it for routine implementation under unchanged design.

## Completion

The gate is complete when both search directions were performed, strong candidates were inspected beyond titles/README, provenance/license boundaries are understood, serious candidates have a disposition, material reasoning is recoverable, and the accepted consequence is represented in `reports/design/`.
