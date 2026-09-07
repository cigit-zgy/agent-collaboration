# Project report and archive contract

Load this reference for repository report-family layout, report filenames/metadata, archive placement, and report cleanup/migration.

## Reports root — hard constraint

When a maintained project uses `reports/`, it may contain only these four direct child directories:

```text
reports/
├── chatgpt/
├── codex/
├── concept/
└── handoff/
```

Each family directory is flat and contains only canonical Markdown artifacts. Do not create nested directories, evidence bundles, images, JSON/YAML sidecars, indexes, or other non-Markdown files under active `reports/`. Supporting task evidence that must be retained belongs in the single repository-root `00_archive/` or another non-report project artifact owner explicitly defined by the project; the report links to that evidence when needed.

No Markdown file or other artifact lives directly under `reports/`. Do not create `reports/archive/`, `reports/00_archive/`, `reports/agent/`, `reports/discussion/`, `reports/integration/`, `reports/review/`, `reports/qualification/`, `reports/pdf2md/`, or another report family. If one of the four families is not used, it may be absent.

Responsibilities are fixed:

```text
reports/chatgpt/ = User + ChatGPT accepted discussion outcome when it becomes a durable FORMAL task/specification
reports/codex/   = Codex execution/verification report bound to a FORMAL task
reports/concept/ = current accepted project design authority when the project declares concepts
reports/handoff/ = conversation migration/context-recovery snapshots only
```

A roadmap, backlog, discussion diary, review log, integration note, qualification note, or historical implementation record is not a fifth report family. Current accepted design belongs in `concept/`; task-specific execution intent belongs in `chatgpt/`; execution evidence belongs in `codex/`; migration continuity belongs in `handoff/`. Historical or superseded material that is not part of the current four-family surface belongs in the repository root archive when retention is justified.

## Execution ownership for report normalization

Report/archive normalization follows the collaboration execution route rather than defaulting to Codex merely because many files move.

```text
connected repository capability is sufficient
AND no User-machine/runtime evidence is required
-> DIRECT: ChatGPT performs the repository migration and connected verification

local filesystem/runtime/tool evidence is genuinely required
-> LOCAL-QUICK or FORMAL as selected by execution.md
```

Bulk Git renames, metadata backfill, path repair, archive relocation, and remote tree verification are still DIRECT when ChatGPT can perform them safely through connected repository capabilities. Do not create a Codex handoff solely for mechanical repository restructuring that does not require local execution.

## Filename contract — hard constraint

Every Markdown artifact under `reports/` uses exactly:

```text
YYMMDD_<family>_NN.md
```

where `<family>` is the directory name:

```text
chatgpt | codex | concept | handoff
```

Examples:

```text
reports/chatgpt/260907_chatgpt_01.md
reports/codex/260907_codex_01.md
reports/concept/260907_concept_01.md
reports/handoff/260907_handoff_01.md
```

`NN` is a two-digit sequence within the same date + family. Do not use semantic filenames, `README.md`, `index.md`, `development-roadmap.md`, or another naming pattern inside `reports/`.

Navigation comes from compact YAML metadata and stable links, not special index filenames. For concept or handoff discovery, select by metadata + filename chronology; an optional current-map/current-handoff artifact must itself obey the same filename contract.

## Common metadata envelope — required

Every report Markdown file begins with YAML front matter containing at least:

```yaml
---
artifact_type: <project_concept | chatgpt_task | codex_report | conversation_handoff>
artifact_id: <YYMMDD_family_NN>
title: <short human-readable title>
date: <YYYY-MM-DD>
project: <project name>
repository: <owner/repository>
status: <family-appropriate status>
summary: >
  <one compact paragraph that allows fast search/recovery>
---
```

Family templates may require additional metadata. Do not remove required task/report/handoff/concept fields merely to satisfy the common envelope. `artifact_id` must equal the filename stem.

Metadata exists to support fast repository search, chronology, authority lookup, and context recovery. Keep it compact; do not duplicate the full body or create a separate status database.

## Concept metadata

A concept artifact additionally identifies its bounded design concern, for example:

```yaml
concept_id: <stable semantic concern id>
role: design_authority
operational_projection:
  - <path>
```

The stable semantic identity lives in `concept_id`, not in the filename. This lets filenames remain uniform while concept topics remain directly searchable.

## ChatGPT / Codex binding

FORMAL task/report pairs retain their task-specific metadata and exact binding. Paths follow the common filename rule:

```text
reports/chatgpt/YYMMDD_chatgpt_NN.md
reports/codex/YYMMDD_codex_NN.md
```

A task that changes maintained Skill behavior still follows:

```text
accepted concept/design
→ committed SKILL.md + references
→ FORMAL task
→ Codex implementation/verification
```

## Handoff discovery

Handoffs live only in `reports/handoff/`. There is no repository-root `handoff/` and no `reports/handoff/README.md` exception.

Each handoff records `previous_handoff` in metadata when one exists. Normal recovery resolves the newest valid handoff by filename chronology/metadata, then reconciles it against current project authority and repository state. Older handoffs are history drill-down only.

## Archive — single-root hard constraint

A maintained repository uses exactly one archive location when archival retention is needed:

```text
<repository-root>/00_archive/
```

Do not create a directory named `archive` anywhere. Do not create nested `*/00_archive/` directories. Historical content displaced from an active responsibility may be retained under the single root archive with its provenance-preserving relative context, for example:

```text
00_archive/reports/<former-family>/...
00_archive/reports/codex_evidence/<artifact-id>/...
```

The `00_` prefix is intentional so the archive sorts first in ordinary filesystem views.

Archive is history only: it is never current design/task/report/runtime authority and is never loaded by default. If retention has no recovery, legal, provenance, or audit value, delete rather than archive.

## Roadmaps and duplicate status files

Do not create `reports/development-roadmap.md` or another parallel design/status authority. Accepted architectural direction, deferred design capability that materially constrains future work, and release/design policy belong in the appropriate current concept topic. Execution backlog without design authority belongs in issues/tasks or another project-declared work-management surface, not a fifth report family.

## Migration / cleanup rule

When normalizing an existing project:

```text
1. inspect current authority and Git history;
2. preserve current four-family artifacts that still carry active authority/evidence/context;
3. rename current report files to the canonical filename form and add/repair required metadata;
4. move repository-root `handoff/` content into `reports/handoff/`;
5. delete obsolete duplicate status/roadmap files when their responsibility is already owned elsewhere;
6. move report-history families and active-report sidecar/evidence bundles that should be retained into root `00_archive/reports/...`;
7. remove all nested directories/non-Markdown sidecars from active report families and remove all nested `archive` / `00_archive` report directories;
8. verify `reports/` has only the four allowed flat families and every Markdown file satisfies filename + metadata rules.
```

Do not rewrite historical scientific/task conclusions merely to modernize formatting. When metadata must be backfilled, preserve body semantics and derive only factual metadata recoverable from the file path/content/Git history; uncertain metadata is stated conservatively rather than invented.
