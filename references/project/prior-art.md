# External prior-art and reuse contract

This contract governs the evidence search that must precede substantial new project design or custom implementation.

## Purpose

Do not invent a project architecture, core algorithm, scientific workflow, or major infrastructure component before checking whether a strong published/open-source precedent already exists.

The default direction is:

```text
search credible prior art
→ inspect the strongest relevant implementations and design rationale
→ decide REUSE | ADAPT | REFERENCE_ONLY | REJECT
→ write or revise the project concept
→ implement only the remaining project-specific gap
```

External prior art is design evidence, not project authority. User + ChatGPT remain the project design decision-makers, and the accepted project concept remains the canonical design authority when the project declares one.

## Trigger — hard gate

Complete this gate before any of the following:

```text
new maintained project
new core subsystem/stage
new major algorithm/modeling method
major architecture redesign
new trust/provenance/state-management mechanism
new substantial framework/dependency/tool choice
custom implementation of a capability likely to exist in mature open source
```

The gate is not required for ordinary bug fixes, typo/documentation edits, small bounded refactors, or direct implementation of an already accepted design unless the change exposes a genuine new design choice.

If the gate applies and has not been completed, ChatGPT MUST NOT freeze a new concept or begin substantial custom implementation. Search first.

## Mandatory two-way search

A gate-triggered design must search in both directions:

```text
literature → code
AND
GitHub/source code → scientific or institutional provenance
```

### Literature → code

Search the most authoritative literature relevant to the actual project domain, then follow Code Availability, Data Availability, supplementary material, author/group links, DOI-linked repositories, Zenodo/software records, or official project pages to the implementation.

For water/environmental/scientific-computing work, explicitly include relevant high-level venues when the topic falls within their scope, for example:

```text
Nature portfolio
- Nature
- Nature Water
- Nature Computational Science
- Nature Communications
- other directly relevant Nature journals

Water / environmental engineering
- Water Research
- Environmental Science & Technology (ES&T)
- Environmental Science & Technology Letters
- other field-leading journals directly relevant to the method
```

These names are search priorities, not automatic authority. A paper without a usable implementation may still inform design, but it is not equivalent to verified reusable code.

Search both recent work and foundational work when each is relevant. Do not use a rigid recency cutoff that would discard established scientific infrastructure.

### GitHub / source code → provenance

Search GitHub and other authoritative source hosts for mature implementations of the required capability. For each serious candidate, determine whether it is linked to:

```text
a peer-reviewed paper or DOI
an author/research-group repository
a journal Code Availability statement
an official scientific organization/foundation/project
a maintained standards ecosystem
```

GitHub stars, forks, or search ranking are maintenance/community signals only; they do not establish scientific authority.

## Source priority

Prefer evidence in this order when relevance is comparable:

1. author-maintained or official code explicitly linked from the peer-reviewed paper/project;
2. official scientific organization, standards body, or long-lived domain project;
3. mature maintained open source with traceable scientific provenance and real users;
4. technically useful repositories with weaker provenance, used only as secondary engineering precedent.

Do not lower scientific/product requirements merely to match a popular repository.

## Candidate inspection

Do not stop at the repository README or paper abstract. For a serious candidate, inspect the materials needed to understand the actual concept and implementation boundary, as available:

```text
paper / methods / supplement
Code Availability / DOI / release record
README and technical docs
architecture/design documents
public API/schema/configuration
core implementation flow
representative tests/examples
release/activity/maintenance state
license
known limitations/issues when material
```

The goal is to recover design precedent, not to copy surface syntax.

For each candidate ask:

```text
What problem boundary does it own?
What are its key objects/stages/interfaces?
What invariants or trust assumptions does it make?
What implementation can be reused directly?
What design pattern can be adapted?
What does not fit this project's scientific/product constraints?
What would still have to be built locally?
```

## Reuse decision

Every materially relevant candidate receives one disposition:

```text
REUSE
= adopt an existing maintained dependency/tool/project with minimal wrapper/adaptation

ADAPT
= reuse a proven architecture/pattern or bounded implementation while changing project-specific semantics

REFERENCE_ONLY
= use as design evidence but do not depend on or copy the implementation

REJECT
= not suitable; record the decisive reason when the candidate was otherwise strong
```

Prefer REUSE or ADAPT over a new custom implementation when they satisfy the accepted scientific/product/trust requirements and licensing/runtime constraints.

A custom implementation is justified only when the prior-art review identifies a concrete gap, incompatibility, trust/reproducibility requirement, or project-specific scientific contract that existing implementations do not satisfy.

## Concept recording — hard requirement

For every gate-triggered project concept, the accepted concept MUST make the prior-art basis recoverable without becoming a literature review.

Use a compact section or table such as:

```text
Prior-art basis

Search scope:
- literature channels / key terms
- GitHub/source channels / key terms

Candidate | Scientific/source provenance | Repository/version | Disposition | Design consequence
...

Result:
- what is reused
- what architecture/pattern is adapted
- what is deliberately not adopted
- the exact remaining gap that justifies custom design
```

Record only the strongest materially relevant candidates. Do not pad the table to an arbitrary count. If no credible candidate exists, record the search scope and that result explicitly.

When exact code is reused or inspected for implementation-level decisions, preserve repository/version/license coordinates sufficient to recover the source. When a paper materially shapes the design, preserve a stable citation/DOI or equivalent source identity.

The concept should cite prior art for the design consequence it supports; it must not copy external project rules wholesale or let external documentation become project authority.

## Licensing and scientific integrity

Design ideas and architecture precedent may be studied broadly. Reusing/copying code requires compatible licensing and attribution obligations to be checked before incorporation.

Do not present an external implementation as scientifically validated merely because it runs, is popular, or accompanies a high-impact paper. Verify that its semantics match the project's intended scientific claim and operating boundary.

## Refresh

Repeat the prior-art gate when:

```text
a new major design concern is introduced
an accepted design is materially reopened
an important tool/dependency is being replaced
new evidence suggests a substantially better established solution exists
```

Do not repeat the full search for routine implementation work under an unchanged accepted concept.

## Completion

The prior-art gate is complete only when:

```text
both search directions were performed
AND strong relevant candidates were actually inspected beyond titles/README summaries
AND provenance + license/reuse boundaries are understood at the level needed for the decision
AND each serious candidate has a disposition
AND the accepted concept records the resulting reuse/adaptation/custom-gap decision
```

Until then, a gate-triggered concept is not ready to freeze.