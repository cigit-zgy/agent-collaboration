# Project conversation handoff contract

This contract governs durable context transfer when a maintained project moves from one ChatGPT conversation/session to another.

## Purpose

A conversation handoff preserves enough project state that a new ChatGPT context can resume work without reconstructing the entire prior conversation.

The handoff is a **context-recovery artifact**, not design authority, task authority, scientific source authority, or implementation evidence.

```text
reports/concept/   = accepted project design authority, when declared
reports/chatgpt/   = committed FORMAL local-execution specification
reports/codex/     = FORMAL execution/verification evidence
reports/handoff/   = conversation continuity and reconstruction context
```

If a handoff conflicts with current concept/task/project authority or current repository state, the current authority/state wins. The handoff records what the prior conversation understood at a specific repository revision.

## Trigger

Create a handoff when any of the following is materially true:

```text
User explicitly requests conversation migration
current conversation is becoming too large or difficult to continue reliably
work intentionally moves to a new conversation/session
project context has become complex enough that a future resume would otherwise require substantial reconstruction
```

Do not create a handoff after every routine task or every conversation message. The artifact exists for meaningful context migration, not as a running diary.

## Ownership

ChatGPT is the primary author of conversation handoffs because the source conversation contains User + ChatGPT design rationale, rejected directions, unresolved questions, and continuity state that Codex does not own.

For a repository-backed project, ChatGPT should create and commit the handoff directly when connected repository capability is sufficient. Do not delegate handoff authorship to Codex merely because the project also uses Codex for LOCAL execution.

Codex may read a handoff for background/context recovery when routed there by project `AGENTS.md`, a FORMAL task, or the User. A handoff MUST NOT override a committed task, accepted concept, project `AGENTS.md`, pinned collaboration authority, or registered scientific source/evidence.

## Stable layout

When a project first needs conversation handoff artifacts, use:

```text
reports/handoff/
├── README.md
├── YYMMDD_handoff_01.md
├── YYMMDD_handoff_02.md
└── ...
```

Do not create the directory for projects that never need conversation migration.

### Handoff filename

Use:

```text
YYMMDD_handoff_NN.md
```

where `NN` is a two-digit sequence for handoffs created on that date or under the project's existing report-numbering convention.

Each issued handoff file is historical evidence of the project state at creation. Do not rewrite old handoffs merely to make them match later design or implementation. Create a new handoff for the next migration.

## Handoff index — required navigation surface

`reports/handoff/README.md` is a **navigation index only**. It is not an additional authority or status database.

Keep it very small. It should contain:

```markdown
# Conversation handoff index

Current handoff: `YYMMDD_handoff_NN.md`

Purpose: context recovery only; current project authority remains in AGENTS/concept/task/source artifacts.

## History

- `YYMMDD_handoff_NN.md` — <short scope/date note>
- `...`
```

Update `Current handoff` whenever a new handoff is committed. Keep history newest first or otherwise deterministic.

Do not place project design rules, execution state machines, task status, or duplicated handoff prose into the index.

## Fast recovery route

For a new ChatGPT conversation/session resuming an existing project:

```text
project AGENTS.md
→ reports/handoff/README.md
→ current handoff only
→ re-resolve current collaboration/project authorities
→ inspect current repository HEAD/state relevant to the resumed work
→ continue
```

The current handoff should be substantially self-contained. A new conversation MUST NOT need to read every previous handoff to understand the current project.

Older handoffs are historical drill-down only. Read them when the current handoff explicitly points to an older unresolved rationale or the User asks for historical reconstruction.

For Codex:

```text
FORMAL task / project AGENTS
→ current task/project authority first
→ current handoff only when additional project context is needed
```

Codex does not preload all handoffs for every task.

## Size guidance

The handoff should be information-dense enough to reconstruct the project but much shorter than the source conversation.

Normal architecture targets:

```text
simple migration          250–400 lines
complex project migration 400–600 lines
major architecture phase  600–800 lines
```

The usual target is **300–600 lines**.

This is guidance, not a parser-enforced line limit. A handoff over roughly 800 lines is a signal to inspect whether concept/task/report text, command logs, or conversation transcript material has been copied unnecessarily.

Do not shorten a handoff so aggressively that accepted rationale, rejected alternatives, unresolved decisions, or next-action state becomes unrecoverable.

## Metadata

Use compact YAML front matter:

```yaml
---
artifact_type: conversation_handoff
handoff_id: <YYMMDD_handoff_NN>
date: <YYYY-MM-DD>
project: <PROJECT_NAME>
repository: <OWNER/REPOSITORY>
source_conversation_title: <TITLE_OR_SHORT_IDENTIFIER>
source_period:
  start: <YYYY-MM-DD_OR_UNKNOWN>
  end: <YYYY-MM-DD>
repository_head: <SHA_AT_HANDOFF_CREATION>
default_branch: <BRANCH>
collaboration_authority: cigit-zgy/agent-collaboration@<SHA>
previous_handoff: <NONE_OR_reports/handoff/...>
source_conversation_url: <OPTIONAL_IF_TRUTHFULLY_AVAILABLE>
---
```

Rules:

- omit `source_conversation_url` when ChatGPT cannot truthfully recover a stable URL;
- do not invent conversation IDs or URLs;
- `repository_head` anchors the repository state understood by the handoff;
- `previous_handoff` supports historical navigation but does not create a required reading chain;
- do not add large metadata inventories that duplicate the body.

## Required information

A handoff should make the following recoverable when applicable. These are information requirements; the headings below are the preferred default because consistency materially improves retrieval across projects.

### 1. Project objective

Capture the stable goal and current success criterion:

```text
what the project is trying to produce
scientific/product/software objective
intended users or consumers when relevant
current high-level completion/success condition
```

Do not turn this into a full project proposal when the concept already owns that material.

### 2. Current system / architecture

Provide the smallest useful current system map, for example:

```text
stage A → stage B → stage C
```

For material stages, summarize only what a new context needs to navigate:

```text
owner
input
output
key trust/interface boundary
current state
```

Use Mermaid or compact tables only when they materially improve recovery.

### 3. Authority map

This is mandatory for maintained projects. Identify the current owning sources needed to resume correctly, for example:

```text
project AGENTS.md
reports/concept/README.md + governing concept topics
workflow SKILL.md / owning references
registered scientific source/evidence authority
current collaboration authority
active FORMAL task, if any
```

State explicitly:

```text
this handoff is context, not design/task/scientific authority
```

### 4. Accepted decisions

Record decisions that would otherwise be expensive to reconstruct or likely to be re-litigated after migration.

Preferred compact shape:

```text
Decision
Current conclusion
Why it was accepted
Rejected alternative(s), when important
Owning authority / source pointer
```

Do not copy the full governing concept. Summarize the design consequence and link to the owner.

### 5. Rejected / superseded directions

Record materially rejected or superseded approaches that a new ChatGPT context might otherwise propose again.

Examples:

```text
rejected architecture
removed compatibility layer
abandoned dependency/tool
superseded naming/state model
explicit non-goal that repeatedly surfaced
```

Keep the decisive reason recoverable.

### 6. Current repository state

Record the state that matters for resumption:

```text
default branch and HEAD at handoff creation
important active task branch(es), if any
latest accepted ChatGPT/Codex task/report relevant to current work
important changed/new files
known unintegrated work
```

Prefer immutable GitHub links for key committed artifacts when available. Do not paste entire task/report bodies.

### 7. Implementation status

Separate design maturity from implementation maturity. Use explicit states such as:

```text
implemented + verified
implemented + awaiting local verification
accepted design + not implemented
in progress
blocked
rejected / removed
```

Do not infer implementation completion from the existence of a concept or Skill document.

### 8. Known problems and unresolved decisions

Classify unresolved work so the next conversation knows who owns the decision:

```text
BLOCKER
OPEN DESIGN — User + ChatGPT decision required
IMPLEMENTATION ISSUE — design fixed; execution remains
EVIDENCE / VERIFICATION GAP
OPTIONAL / FUTURE
```

Do not silently resolve an open design question inside the handoff.

### 9. Current evidence / important artifacts

List only artifacts materially useful for continuing the work:

```text
concept files
ChatGPT task(s)
Codex report(s)
important commit(s)/PR(s)/issue(s)
scientific paper DOI/source
external repository + commit/release
important user-provided file names
```

Prefer stable identifiers/links over copied content.

### 10. Next actions

Give the next conversation an executable continuation order.

For example:

```text
Next 1 — ...
Next 2 — ...
Next 3 — ...

Do not start yet:
- ...
```

Separate tasks ChatGPT can execute DIRECT from tasks that genuinely require Codex LOCAL work.

### 11. Project-specific User constraints

Record only project-relevant working constraints that materially change future decisions or execution, for example:

```text
required scientific rigor/boundary
accepted tooling preference
ChatGPT-first authoring expectation
Codex/local verification boundary
temporary workspace restrictions
output/report preferences
```

Do not copy irrelevant personal information or global collaboration rules already recoverable from current authority.

### 12. Source pointers / raw provenance

Preserve enough raw provenance to trace the summary back to durable material without copying the full conversation.

Include, when truthfully available and materially relevant:

```text
source conversation title/identifier
source conversation time range
source conversation URL
repository + branch + handoff HEAD
collaboration commit
concept/task/report paths + immutable commit links
important PR/issue/commit links
paper DOI / stable citation
external repository + immutable revision/release
important user-provided source filenames
previous handoff path
```

A full chat transcript is not required and should not be copied into the repository merely for completeness.

## Default body template

```markdown
# Conversation handoff — <project / phase>

## 1. Project objective

## 2. Current system / architecture

## 3. Authority map

## 4. Accepted decisions

## 5. Rejected / superseded directions

## 6. Current repository state

## 7. Implementation status

## 8. Known problems and unresolved decisions

## 9. Current evidence / important artifacts

## 10. Next actions

## 11. Project-specific User constraints

## 12. Source pointers / raw provenance
```

A section may be short or omitted only when it genuinely has no useful content; do not fill empty sections with `N/A` ceremony.

## Creation procedure

When producing a handoff, ChatGPT should:

```text
1. resolve the current project/collaboration authority for the migration work unit;
2. inspect current repository state and the governing concept/task/report artifacts relevant to the active work;
3. summarize the source conversation independently rather than copying long stretches verbatim;
4. distinguish accepted design, implementation state, evidence, and unresolved decisions;
5. create the new handoff file;
6. update reports/handoff/README.md current pointer/history;
7. commit/push the handoff artifacts;
8. give the User the committed handoff path/link and a minimal instruction for starting the new conversation when useful.
```

The handoff must not become a second concept or second Codex report.

## Recovery validation

A handoff is ready when a fresh Agent can answer, from the current handoff plus current project authority:

```text
What is the project trying to do?
What architecture/state exists now?
Which files are authoritative?
What important decisions are already settled, and why?
What approaches were explicitly rejected?
What is implemented versus only designed?
What remains unresolved, and who owns each decision?
What should happen next?
Where can the underlying evidence be found?
```

If answering these questions requires reading several older handoffs or reconstructing the source conversation, the current handoff is insufficient.

## Staleness and reconciliation

A handoff is a snapshot at `repository_head` and creation time. On resume, the new ChatGPT/Codex context MUST reconcile it against current repository/authority state before making substantive changes.

Do not silently assume:

```text
handoff repository_head == current HEAD
handoff concept pointers are still current
handoff open questions are still unresolved
handoff task branch is still active
```

Use the handoff to recover context, then use current authority to decide what is true now.
