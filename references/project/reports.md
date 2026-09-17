# Project report and governance-artifact contract

Load this reference for `reports/` layout, append-only work records, living-Design placement, conversation handoff, and archive placement.

## Reports root

For ordinary long-running projects the active report surface is:

```text
reports/
├── design/      current living Design; mutable current authority
├── chatgpt/     append-only ChatGPT work records
├── codex/       append-only Codex execution records
├── concept/     append-only explicit User-requested reasoning history
└── handoff/     append-only conversation-boundary handoffs
```

Do not create additional active families such as `reports/verification/`, `reports/review/`, or `reports/status/` merely to classify evidence.

Verification is an evidence role, not a report family:

```text
maintained test logic       → tests/
FORMAL/LOCAL execution record → reports/codex/
one-off disposable outputs  → tmp/
historical retained material with no current consumer → 00_archive/
```

## Current versus historical

```text
reports/design/
= current accepted result
= replace-in-place

chatgpt / codex / concept / handoff
= historical records
= append-only
```

Git history preserves Design evolution; Reports preserve the work that led there.

## Chronological families

The four historical families are flat and use:

```text
YYMMDD_<family>_NN.md
```

where `<family>` is `chatgpt | codex | concept | handoff`.

Do not overwrite or repurpose an issued historical artifact. Later work gets a new file.

## Common metadata

New report artifacts carry the smallest useful common envelope:

```yaml
---
artifact_type: <chatgpt_record | codex_report | project_concept | conversation_handoff>
artifact_id: <YYMMDD_family_NN>
record_kind: <family-specific kind>
title: <short title>
date: <YYYY-MM-DD>
project: <project>
repository: <owner/repository>
status: <family-appropriate status>
summary: >
  <compact searchable summary>
design_topics: []
baseline_sha: <optional repository baseline>
result_sha: <optional resulting repository state>
design_signal: <none | design_change | design_drift | design_gap>
---
```

Only include optional coordinates when they are meaningful. Existing historical files do not need bulk rewriting merely to add newer metadata fields.

## ChatGPT records

`reports/chatgpt/` preserves substantive ChatGPT work that future reconstruction may need.

Use:

```text
record_kind: task        durable Codex task specification
record_kind: direct      material ChatGPT DIRECT design/code/repository work
record_kind: acceptance  material acceptance/adjudication result
```

Every delegated Codex repository task remains a durable `task` record before execution. Trivial conversation turns do not require a report.

## Codex records

Every Codex repository task leaves a `reports/codex/YYMMDD_codex_NN.md` record.

```text
LOCAL-QUICK → concise execution record
FORMAL      → full execution/evidence report
```

Both preserve what actually changed, final repository coordinates, material evidence, limitations, and any Design signal. LOCAL-QUICK records stay short; FORMAL records carry the detail required by `formal.md`.

## Concept family

A new Concept is created only after explicit User instruction under `concept.md`.

Concept preserves historical reasoning; it is never current authority. A requested Concept that changes accepted Design is complete only after current Design is updated in the same work unit.

## Handoff family

When the User explicitly ends/replaces a long conversation (`换对话框` or equivalent), create one compact handoff after accepted state, reports, and CURRENT are durable.

Handoff summarizes the conversation boundary and report ranges; it does not replace Design, CURRENT, or the underlying reports. Detailed rules live in `handoff.md`.

## Design exception

`reports/design/` is not a chronological family. It is governed by `design.md` and `reconciliation.md`.

Self-hosting Skill/policy repositories may intentionally keep current operational authority in `SKILL.md + references/` instead of duplicating it into `reports/design/`; `design.md` defines that exception.

## CURRENT and archive

`CURRENT.md` remains repository-root mutable NOW-state and points to owners rather than duplicating them.

Historical retention with no current owner uses one repository-root `00_archive/`. Archive is cold and never current authority.

## Responsibility map

```text
current accepted Design              → reports/design/ or declared self-hosting current owner
ChatGPT substantive work             → reports/chatgpt/
Codex execution work                 → reports/codex/
explicit User-requested rationale    → reports/concept/
conversation-boundary continuity     → reports/handoff/
current work edge                    → CURRENT.md
maintained verification logic        → tests/
historical retained material        → 00_archive/
```

Design reconciliation from accumulated reports is owned by `reconciliation.md`.
