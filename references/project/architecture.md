# Project architecture and integration contract

This contract governs how a maintained scientific/software project joins `agent-collaboration` and how repository responsibilities are separated.

## Project entry

Root `AGENTS.md` is the project-local constitution. It identifies project identity, authority, ownership boundaries, workflow entry, runtime authority, and genuine human/trust checkpoints. Use `../collaboration/agents.md` plus `templates/agents.md` when authoring it.

A project workflow Skill may live at any project-declared path; it is not required to be repository-root `SKILL.md`.

## Responsibility-based architecture

There is no universal or canonical project filesystem in this collaboration standard.

A project creates only responsibilities that have a real owner, artifact, and consumer. Common ownership patterns include:

| Responsibility | Common path | Meaning |
|---|---|---|
| project constitution | `AGENTS.md` | repository-scoped authority and routing |
| human orientation | `README.md` | human-facing introduction/quick start |
| runtime/tooling authority | `pyproject.toml` or project-declared equivalent | dependencies/tooling when a runtime exists |
| Agent capability package | `<agent-name>/` | project-owned workflow/sub-Skills when present |
| reusable implementation | `src/` | reusable executable code/infrastructure |
| durable model artifacts | `models/` | project-adopted model-specific definitions/artifacts |
| canonical reusable data | `data/` | project-adopted datasets |
| mutable work state | `workspace/` | current case/model/Agent operational state |
| controlled investigations | `experiments/` | reproducible calibration/simulation/benchmark/case-study work |
| conformance/regression checks | `tests/` | tests for stable contracts/implementation |
| human technical documentation | `docs/` | durable explanation beyond README |
| publication assets | `manuscript/` | manuscript/figure/supplement materials when owned here |
| accepted project design | `reports/concept/` | canonical design only when the project declares it |
| formal delegated tasks | `reports/chatgpt/` | committed local-execution specifications |
| Codex execution evidence | `reports/codex/` | formal execution/verification reports |

These paths are examples of common ownership patterns, not required directories. A project may use different paths when its `AGENTS.md` declares equivalent ownership clearly.

## Design authority

When a scientific project declares `reports/concept/` as canonical design authority, the writing, review, adjudication, freeze, and projection lifecycle is owned by `concept.md`.

This architecture contract only requires that project-local authority and operational ownership remain explicit; it does not restate the concept contract.

Model-specific scientific facts remain grounded in the project's registered source/evidence chain rather than in repository-architecture documents.

## Runtime reading route

For ordinary Agent operation, the project should expose the shortest stable route:

```text
AGENTS.md
→ declared workflow SKILL.md
→ owning sub-Skill
→ required reference/script
```

Design/redesign/conformance work follows the design-authority route defined in `concept.md` when the project uses canonical concepts.

## Ownership boundaries

Use responsibilities rather than folder symmetry:

```text
reusable engine/algorithm/API → reusable implementation owner
model-specific durable object → model-artifact owner
canonical reusable dataset    → data owner
mutable current run state      → workspace owner
controlled investigation      → experiment owner
```

Promotion between responsibilities is explicit. Experiment outputs become canonical data/model artifacts only after project adoption with provenance. Exploratory code becomes reusable implementation only when a real reusable consumer and stable contract exist. Live workspace state remains mutable even when captured as an experiment input/snapshot.

## External tool integration boundary

Third-party scientific/software tools must be integrated through an explicit adapter boundary when their CLI, API, file layout, schema, or runtime behavior is implementation-specific and may evolve independently of the project.

The project design layer defines what capability and artifact semantics are required; it should not unnecessarily freeze transient third-party command spelling.

The normal ownership model is:

```text
project concept / contract
→ required capability and artifact semantics

owning adapter
→ concrete CLI/API/schema knowledge
→ version/profile compatibility checks
→ invocation and output discovery

other project modules
→ consume the adapter's project-facing result
→ do not duplicate third-party interface details
```

Concrete third-party flags, endpoint paths, native output filename patterns, or schema branching should have one implementation owner. Do not scatter the same external interface knowledge across orchestration code, Skills, multiple helpers, and tests unless each occurrence is an intentionally bounded contract assertion.

### Known-profile verification

For an evolving external interface, prefer an explicit known-compatible profile plus verification over speculative runtime adaptation.

A compatibility probe may inspect stable surfaces such as:

```text
--version
--help
capability metadata
API version endpoint
schema/version marker
```

but the probe verifies that a known profile is supported; it does not infer a new interface automatically.

If an expected flag, endpoint, schema, artifact, or semantic capability changes in a way the adapter does not understand:

```text
unknown / semantically incompatible external profile
→ fail closed
→ report the unsupported interface
→ update + revalidate the adapter explicitly
```

Do not guess a renamed flag, select a merely plausible replacement, silently switch tools/backends, or reinterpret changed option semantics just because an invocation can be made to run.

### Scientific reproducibility

For scientific preprocessing, conversion, simulation, or other result-bearing tools, successful execution is not sufficient evidence of semantic compatibility. The project should record the tool/version/configuration facts that materially affect reproducibility when those facts are part of the produced result's provenance.

Version pinning is not universally required. Use a fixed version when the project needs exact-environment reproduction; otherwise a validated compatible profile may be sufficient. In both cases, speculative forward compatibility is subordinate to reproducibility and explicit semantics.

## Project onboarding

```text
inspect actual repository
→ establish/normalize project AGENTS.md
→ declare real ownership and runtime boundaries
→ define accepted design authority when the project needs one
→ expose workflow Skill only when a repeatable Agent workflow exists
→ project Skills/references operationalize accepted design
→ implementation follows the projection
→ tests verify conformance
→ Codex is delegated only for genuinely local execution/verification
```

Project collaboration routes to `../collaboration/protocol.md` rather than copying global collaboration, Git, task/report, or verification manuals into each repository.

## Review criterion

A project architecture is sufficient when an unfamiliar Agent can determine the repository's real owners, authority sources, workflow entry, mutable-state boundaries, design/scientific-fact distinction, and external-tool adapter boundaries without inferring a standard directory tree or hidden third-party compatibility behavior that the project does not actually use.
