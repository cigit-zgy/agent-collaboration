# GitHub Actions and hosted-CI contract

Load this reference only when deciding whether a GitHub-hosted workflow should exist, what it should trigger on, or whether it duplicates ChatGPT/Codex evidence.

GitHub Actions is an **independent hosted evidence environment**, not the default place to repeat development checks already proven elsewhere.

## Claim-deduplication — hard requirement

```text
same verification claim
+ already proven in an appropriate environment
→ do not repeat it in GitHub Actions

distinct hosted-environment claim
→ GitHub Actions may be justified
```

A command is not a claim. Running `ruff`, `pytest`, type checking, package build, LaTeX rendering, or another command in Actions is justified only when the hosted execution proves something materially distinct.

Typical distinct hosted claims include:

```text
clean-room build/install independent of the User machine
supported OS/Python/runtime matrix
PR/merge status gate that must exist on GitHub
release/tag/package/publish automation
open-source reproducibility visible to external contributors
release/security evidence intentionally requiring an independent environment
```

If Codex already proves the same claim locally and no distinct hosted claim remains, the Actions run is redundant.

## Private repositories

Ordinary development defaults to:

```text
ChatGPT authoring / cheap connected checks
→ Codex local verification
→ ChatGPT acceptance
```

Automatic `push`/`pull_request` Actions SHOULD be absent by default in private repositories.

Enable private-repository Actions only when a workflow owns a concrete distinct claim worth the account's current Actions budget. Prefer the narrowest trigger and matrix that proves it:

```text
workflow_dispatch for milestone / clean-room checks
release/tag trigger for release qualification
path filters when only a bounded area matters
concurrency + cancel-in-progress when repeated automatic runs are genuinely required
smallest supported runtime/OS matrix sufficient for the claim
```

Do not maintain a broad multi-OS/multi-version matrix on every private-repository push merely for reassurance.

## Public repositories

Public repositories may retain standard GitHub-hosted CI when it materially improves public reproducibility, contributor feedback, status checks, packaging, or release confidence.

Budget pressure alone is not a reason to remove standard public-repository CI when GitHub's current billing model does not charge the account's included private-repository minutes for those standard public runs. Billing and runner pricing are external platform facts and MUST be rechecked against current official GitHub documentation whenever they materially affect a decision.

Public status does not waive claim deduplication. Free redundant CI is still redundant engineering work.

Special/larger runners, storage, artifacts, caches, and other billable platform resources are separate concerns; do not infer their cost from standard-runner policy.

## Review triggers

Review Actions configuration when:

```text
repository visibility changes
Actions usage/budget becomes material
new automatic workflow is introduced
runtime matrix grows
Codex begins proving the same claims locally
release/publication workflow changes
```

For each workflow/job ask:

1. What exact claim does it prove?
2. Is that claim already proven by ChatGPT/Codex/project tooling?
3. Does GitHub-hosted execution provide a distinct environment/status/release property?
4. Is trigger frequency proportional to the claim?
5. For private repositories, is the expected budget cost justified?

If a workflow cannot answer those questions, remove, narrow, or make it manual.

## Relationship to verification levels

This file decides **whether hosted execution is warranted**. Verification rigor and evidence categories remain owned by `verification.md`.

A LEVEL 3 release may justify Actions, but LEVEL 3 does not automatically require Actions. Likewise, a LEVEL 1 task may use an existing hosted status check when that check is already the cheapest valid evidence.

Do not load `verification.md` merely to decide a simple Actions budget/duplication question; load both only when the task also requires verification-level/evidence design.
