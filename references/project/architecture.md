# Project architecture and integration contract

This contract governs how a maintained scientific/software project joins `agent-collaboration` and how repository responsibilities are separated.

## Project entry

Root `AGENTS.md` is the project-local constitution. It identifies project identity, authority, ownership boundaries, workflow entry, runtime/tooling authority, and genuine human/trust checkpoints. Use `../collaboration/agents.md` plus `templates/agents.md` when authoring it.

A project workflow Skill may live at any project-declared path; it is not required to be repository-root `SKILL.md`.

## Responsibility-based architecture

There is no universal or canonical project filesystem in this collaboration standard.

Create only responsibilities that have a real owner, artifact, and consumer. Common patterns include:

| Responsibility | Common path | Meaning |
|---|---|---|
| project constitution | `AGENTS.md` | repository-scoped authority and routing |
| human orientation | `README.md` | human-facing introduction/quick start |
| runtime/tooling authority | `pyproject.toml` or project-declared equivalent | dependencies, mechanical style, tooling when a runtime exists |
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
| formal delegated tasks | `reports/chatgpt/` | committed FORMAL local-execution specifications |
| Codex execution evidence | `reports/codex/` | FORMAL implementation/verification reports |
| Agent-local temporary state | `tmp/` | sole project-local scratch/test/worktree/download/cache/render/disposable-env boundary |

These are examples, not required directories. Equivalent ownership is valid when the project `AGENTS.md` makes it explicit, except that Agent-created ephemeral local state follows the `tmp/` boundary below unless the User explicitly authorizes another location.

## Design authority

When a scientific project declares `reports/concept/` as canonical design authority, `concept.md` owns the writing, review, adjudication, freeze, and projection lifecycle.

Model-specific scientific facts remain grounded in the project's registered source/evidence chain rather than repository-architecture documents.

## Runtime reading route

For ordinary Agent operation, expose the shortest stable route:

```text
AGENTS.md
→ declared workflow SKILL.md
→ owning sub-Skill
→ required reference/script
```

Design/redesign/conformance work follows the design-authority route in `concept.md` when applicable.

AI-assisted executable implementation follows `../collaboration/implementation.md`; project tooling/CI remains the owner of language-specific mechanical style and checks.

## Ownership boundaries

Use responsibilities rather than folder symmetry:

```text
reusable engine/algorithm/API → reusable implementation owner
model-specific durable object → model-artifact owner
canonical reusable dataset    → data owner
mutable current run state      → workspace owner
controlled investigation      → experiment owner
Agent-created ephemeral state → tmp owner
```

Promotion between responsibilities is explicit. Experiment outputs become canonical data/model artifacts only after project adoption with provenance. Exploratory code becomes reusable implementation only when a real reusable consumer and stable contract exist. Live workspace state remains mutable even when captured as an experiment input/snapshot.

## Project-local ephemeral workspace — hard boundary

For LOCAL execution, every temporary artifact intentionally created by ChatGPT/Codex tooling on the User machine MUST remain inside the target project's root `tmp/` tree unless the User explicitly names another location.

Default work isolation:

```text
<PROJECT_ROOT>/tmp/<WORK_ID>/
```

`WORK_ID` means:

```text
FORMAL      → exact task_id
LOCAL-QUICK → short local work/session label that is unique enough within the project
```

Create only the subdirectories actually needed, for example:

```text
worktree/   linked FORMAL worktree when needed
run/        scratch execution/test/E2E output
downloads/  disposable downloads
cache/      task-local cache
renders/    temporary render artifacts
env/        disposable environment only when explicitly justified
```

The boundary covers Agent-chosen linked worktrees, scratch repositories, temporary downloads, test outputs, render outputs, caches, intermediate files, and disposable environments. Agents MUST NOT create persistent sibling project directories, Desktop test folders, Documents-root scratch directories, ad-hoc global temporary workspaces, or similarly scattered task state merely for convenience.

Examples of non-conforming Agent-created paths include:

```text
../<project>-<sha>/
../<project>-<task>/
~/Desktop/tests/
~/Documents/<project>-scratch/
/tmp/<project>-persistent-test/
```

System/runtime caches whose location is controlled by the operating system or an external tool and cannot reasonably be redirected are outside this ownership rule; the Agent must not deliberately choose them as project scratch space.

When `tmp/` exists in a maintained repository, it should normally be excluded from version control with a root-scoped ignore such as `/tmp/`. Do not commit task scratch state.

Cleanup lifecycle:

```text
completed + no recovery value
→ remove work tmp immediately

BLOCKED/FAIL + deliberate recovery value
→ retain only the minimum needed state and report why

superseded/cancelled + no recovery value
→ remove work tmp

active/dirty/unpushed/uncertain state
→ preserve until safety is established
```

No age threshold alone authorizes deletion. A retained recovery workspace should normally be reconsidered on the next local task in that project; stale task state with no recovery value should be removed rather than accumulated.

Git linked worktrees are removed through Git-aware operations (`git worktree remove` followed by `git worktree prune` when appropriate), not by blind filesystem deletion. Never destroy dirty, unpushed, active, or ambiguous User state merely to satisfy cleanup.

## External tool integration boundary

Third-party scientific/software tools use an explicit adapter boundary when their CLI, API, file layout, schema, or runtime behavior is implementation-specific and may evolve independently.

The project design layer defines required capability and artifact semantics; it should not unnecessarily freeze transient command spelling.

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

Concrete flags, endpoint paths, native output filename patterns, or schema branching should have one implementation owner. Duplicate external-interface knowledge only when a second occurrence is an intentionally bounded contract assertion.

### Known-profile verification

For an evolving external interface, prefer an explicit known-compatible profile plus verification over speculative runtime adaptation.

A probe may inspect stable surfaces such as:

```text
--version
--help
capability metadata
API version endpoint
schema/version marker
```

The probe verifies a known profile; it does not infer a new interface automatically.

If an expected capability changes in a way the adapter does not understand:

```text
unknown / semantically incompatible external profile
→ fail closed
→ report unsupported interface
→ update + revalidate adapter explicitly
```

Do not guess renamed flags, select merely plausible replacements, silently switch tools/backends, or reinterpret changed semantics because an invocation happens to run.

### Scientific reproducibility

For result-bearing scientific tools, successful execution is not evidence of semantic compatibility by itself. Record tool/version/configuration facts that materially affect reproducibility when those facts are part of result provenance.

Exact version pinning is not universal. Use a fixed version for exact-environment reproduction; otherwise a validated compatible profile may be sufficient. In both cases, reproducibility and explicit semantics outrank speculative forward compatibility.

## Project onboarding

```text
inspect actual repository
→ establish project AGENTS.md
→ declare real ownership + runtime/tooling boundaries
→ define accepted design authority when needed
→ expose workflow Skill only when a repeatable Agent workflow exists
→ project Skills/references operationalize accepted design
→ AI-assisted implementation follows implementation.md + project tooling
→ tests/evidence verify conformance
→ route LOCAL work through LOCAL-QUICK or FORMAL according to protocol risk
```

Project collaboration routes to `../collaboration/protocol.md`, `../collaboration/implementation.md`, and `../collaboration/verification.md` rather than copying those manuals into every repository.

## Review criterion

A project architecture is sufficient when an unfamiliar Agent can determine the real owners, authority sources, workflow entry, mutable-state boundaries, ephemeral-state boundary, design/scientific-fact distinction, implementation/tooling authority, and external-tool adapter boundaries without inferring a canonical directory tree or hidden compatibility behavior.
