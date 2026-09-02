---
id: 04
title: Canonical Skill Package Architecture
status: active
created: 2026-09-02
updated: 2026-09-02
authority: global
scope: Skill source repositories, portable distribution bundles, purpose profiles, AGENTS ownership, progressive disclosure, and initialization rules
supersedes: null
related_tasks: []
---

# Canonical Skill Package Architecture

## Current conclusion

A reusable Skill is a bounded capability package, not a general research or software
project. Skill runtime and Skill source-repository maintenance are distinct
boundaries.

The portable Skill distribution has one structurally required file, root `SKILL.md`;
`references/`, `scripts/`, and `assets/` are optional runtime resources with real
consumers:

```text
portable Skill distribution
├── SKILL.md              # required
├── references/           # optional
├── scripts/              # optional
└── assets/               # optional
```

A standalone first-party Skill that is maintained as its own source repository keeps
a persistent root `AGENTS.md` in addition to the runtime Skill entry:

```text
maintained first-party Skill repository
├── AGENTS.md             # repository-maintenance constitution
├── SKILL.md              # Agent-facing Skill runtime entry
├── references/           # optional
├── scripts/              # optional
├── assets/               # optional
├── tests/                # optional maintenance verification
├── pyproject.toml        # optional independent runtime authority
└── README.md             # optional human-facing documentation
```

`AGENTS.md` is not deleted when the Skill becomes mature. It remains the maintenance
constitution for future Agents working on the source repository. It is not, however,
a required component of a portable Skill distribution and may be omitted by a
packaging/install boundary that ships only operational Skill resources.

An embedded sub-Skill normally inherits the nearest applicable parent/project
`AGENTS.md` and does not receive another one merely for symmetry. A nested
`AGENTS.md` exists only when that subtree has genuine narrower maintenance rules.
Third-party Skills preserve upstream structure and are not normalized to these
first-party conventions.

Purpose profile is independent of `AGENTS.md` ownership. First-party Skill creation
uses four capability profiles:

```text
documentation
executable
asset-oriented
composite/router
```

The canonical package/source architecture is documented in
`references/skill-package-architecture.md`. The maintained first-party Skill
repository constitution scaffold lives in `references/skill-agents-template.md`.
Purpose-specific `SKILL.md` scaffolds live under `references/skill-templates/`.

Skill discovery and operation use progressive disclosure:

```text
name/description
→ SKILL.md
→ only relevant references/scripts/assets
→ execute only the active branch
```

Repository-maintenance Agents first obey the applicable `AGENTS.md` before modifying
the source repository.

## Decision history

### 2026-09-02 — initial package profiles

#### Conclusion

The Skill development standard was split into three concerns:

```text
skill-repository-policy.md
= ownership, local/GitHub placement, first-party vs third-party

skill-package-architecture.md
= package contents and creation conditions

skill-templates/
= purpose-specific SKILL.md scaffolds
```

The four purpose profiles were fixed as Documentation, Executable, Asset-oriented,
and Composite/router. Optional directories are created only when a real consumer
exists.

#### Rationale

A single mandatory directory tree causes empty folders, unnecessary runtimes, and
speculative abstractions. A minimal core plus conditional extensions preserves
portability and progressive disclosure while allowing executable first-party Skills
to use normal software-engineering verification where it is actually needed.

#### Boundary

This decision defined capability/package shape but did not yet fully distinguish a
maintained Git source repository from a portable runtime Skill bundle.

#### Impact

- `references/skill-package-architecture.md`
- `references/skill-templates/`
- `references/skill-repository-policy.md`

#### Related tasks

None.

### 2026-09-02 — source repository versus distribution bundle

#### Conclusion

The maintenance and runtime boundaries are now explicit:

```text
maintained source repository
≠
portable Skill distribution bundle
```

A maintained standalone first-party Skill repository requires root `AGENTS.md` under
our collaboration policy. That file governs future repository development and
maintenance, while root `SKILL.md` governs Agent use of the capability. Maturity does
not remove `AGENTS.md` from the source repository.

A portable Skill distribution does not require `AGENTS.md`; it contains `SKILL.md`
and only the runtime resources required by the capability. Embedded sub-Skills
normally inherit the parent `AGENTS.md`; third-party Skills preserve upstream
structure.

Capability profile does not determine `AGENTS.md` presence. Repository ownership and
maintenance scope do.

The first-party initialization path is therefore:

```text
classify ownership
→ define capability boundary
→ if standalone maintained FIRST_PARTY: create root AGENTS.md
→ choose purpose profile
→ create SKILL.md
→ add only justified references/scripts/assets/tests/runtime
→ distinguish source-only maintenance assets from portable distribution resources
```

#### Rationale

`AGENTS.md` and `SKILL.md` serve different consumers and lifecycles. Conflating them
creates two opposite errors: deleting useful long-term repository instructions when a
Skill matures, or shipping repository-maintenance instructions as if they were a
required portable Skill runtime component.

The source/distribution distinction also explains why a complex first-party Skill
repository may legitimately contain tests, reports, CI, or human-facing docs that do
not belong in the installed Skill package.

#### Boundary

This policy does not claim that external Agent Skills standards require
`AGENTS.md`. The root `AGENTS.md` requirement is our maintained first-party repository
policy. Portable Skill compatibility continues to depend on `SKILL.md` plus the
operational resources actually required by the Skill.

This concept still does not define full scientific/research project architecture;
that will be governed separately.

#### Impact

- root `AGENTS.md` of `agent-collaboration`
- `references/skill-agents-template.md`
- `references/skill-package-architecture.md`
- `references/skill-repository-policy.md`
- `references/skill-templates/README.md`
- `SKILL.md` onboarding/routing
- future first-party Skill initialization, maintenance, packaging, and audits

#### Related tasks

None. User + ChatGPT settled the boundary and ChatGPT applied it directly through
connected repository tooling because no local-machine execution was required.
