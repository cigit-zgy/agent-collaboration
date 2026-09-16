# External prior-art and reuse contract

This contract governs evidence search before substantial new project design or custom implementation.

## Purpose

Do not invent a project architecture, core algorithm, scientific workflow, major infrastructure component, or substantial reusable utility before checking strong published/open-source precedents.

```text
search credible prior art
→ inspect strongest implementations/rationale
→ decide REUSE | ADAPT | REFERENCE_ONLY | REJECT
→ record exploration in reports/concept/ only when the User explicitly requests Concept persistence
→ reduce accepted consequence into reports/design/
→ implement only the remaining project-specific gap
```

External prior art is evidence, not project authority. User + ChatGPT remain design decision-makers. Current accepted design lives in `reports/design/`.

## Trigger

Run this gate for a new maintained project/core subsystem/major algorithm or modeling method/major architecture redesign/new trust-provenance-state mechanism/substantial framework or dependency choice/custom capability likely to exist in mature open source.

Ordinary bug fixes, typo/docs edits, bounded refactors, and direct implementation of already accepted design do not require reopening the gate unless a genuine new design choice appears.

If the gate applies, do not accept the design into `reports/design/` or begin substantial custom implementation until the search/reuse decision is complete.

## Mandatory two-way search

Search both when scientific provenance materially matters:

```text
literature → code
AND
GitHub/source → scientific or institutional provenance
```

For scientific/environmental work, prioritize directly relevant high-level venues and original institutional/author sources when in scope, without treating venue prestige as automatic authority.

## Candidate priority

When relevance is comparable, prefer:

```text
official / standards-body / original-author implementation
→ long-lived domain or scientific-organization project
→ mature actively maintained OSS
→ weaker-provenance repositories only as secondary precedent
```

Then evaluate:

```text
recent maintenance / compatible releases
API and semantic fit
license and security posture
documentation and tests
release stability and ecosystem adoption
stars / forks / downloads as supporting popularity signals
```

Stars and similar metrics are useful secondary signals, not hard admission thresholds. A niche authoritative scientific library may have modest stars; a high-star repository may be stale, insecure, unlicensed, or semantically wrong for the project.

Prefer REUSE/ADAPT when a maintained dependency materially reduces custom implementation and maintenance burden without violating scientific/product semantics, reproducibility, licensing, security, deployment, or runtime constraints.

Do not add a heavy dependency for a trivial capability when a small direct implementation is clearer and cheaper to maintain.

## Candidate inspection

For serious candidates inspect enough to recover the actual boundary: provenance, release/maintenance state, docs, architecture/API/schema/config, representative tests/examples, license, security-relevant signals, and material limitations.

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
REJECT         unsuitable; retain only the decisive reason when it matters
```

## Recording and reduction

Preserve dependency provenance/version/license coordinates where needed for reproducibility. Detailed search/reasoning goes to `reports/concept/` only when the User explicitly asks to persist Concept history.

After adjudication:

```text
reports/design/ = accepted current semantics only
implementation = reuse/adapt/custom gap according to the accepted disposition
```

Do not copy rejected alternatives or chronological search narrative into living Design.

## Refresh

Repeat the gate when a major concern is introduced/reopened, an important tool/dependency is replaced, or new evidence suggests a substantially better established solution. Do not repeat it for routine implementation under unchanged design.

## Completion

The gate is complete when strong candidates were inspected beyond titles/README, provenance/maintenance/license/security boundaries are understood, serious candidates have a disposition, and the accepted consequence is represented in current Design when design-bearing.
