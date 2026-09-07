# Conversation handoff authoring template

Load this template only when ChatGPT is creating a new project conversation handoff. Context recovery does not need this file.

## Size guidance

The handoff should be information-dense enough to reconstruct the project but much shorter than the source conversation.

```text
simple migration          250–400 lines
complex project migration 400–600 lines
major architecture phase  600–800 lines
```

The usual target is 300–600 lines. This is guidance, not a parser-enforced line limit.

A handoff above roughly 800 lines is a signal to inspect whether concept/task/report text, command logs, or conversation transcript material has been copied unnecessarily.

Do not shorten so aggressively that accepted rationale, rejected alternatives, unresolved decisions, or next-action state becomes unrecoverable.

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

- omit `source_conversation_url` when no stable truthful URL is available;
- do not invent conversation IDs or URLs;
- `repository_head` anchors the repository state understood by the snapshot;
- `previous_handoff` supports history navigation but does not create a required reading chain;
- do not add metadata inventories that duplicate the body.

## Default body

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

A section may be short or omitted only when it genuinely has no useful content. Do not fill empty sections with `N/A` ceremony.

## Section requirements

### 1. Project objective

Capture the stable project goal, scientific/product/software objective, intended consumers when relevant, and current high-level success condition. Do not copy the full proposal when the concept already owns it.

### 2. Current system / architecture

Provide the smallest useful system map. For material stages, summarize only what a new context needs to navigate:

```text
owner
input
output
key trust/interface boundary
current state
```

Use Mermaid or tables only when they materially improve recovery.

### 3. Authority map

Mandatory for maintained projects. Identify the current owning sources needed to resume correctly, such as:

```text
project AGENTS.md
reports/concept/README.md + governing concept topics
workflow SKILL.md / owning references
registered scientific source/evidence authority
current collaboration authority
active FORMAL task, if any
```

State explicitly that the handoff is context, not design/task/scientific authority.

### 4. Accepted decisions

Record decisions expensive to reconstruct or likely to be re-litigated after migration.

Preferred compact shape:

```text
Decision
Current conclusion
Why it was accepted
Rejected alternative(s), when important
Owning authority / source pointer
```

Summarize the design consequence and link to the owner; do not copy the whole concept.

### 5. Rejected / superseded directions

Preserve materially rejected or superseded approaches that a new context might otherwise propose again, including decisive reason.

### 6. Current repository state

Record only resumption-relevant state:

```text
default branch + HEAD
important active task branches
latest accepted task/report relevant to current work
important changed/new files
known unintegrated work
```

Prefer immutable links for committed artifacts. Do not paste complete task/report bodies.

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

### 8. Known problems and unresolved decisions

Classify so the next context knows the owner:

```text
BLOCKER
OPEN DESIGN — User + ChatGPT decision required
IMPLEMENTATION ISSUE — design fixed; execution remains
EVIDENCE / VERIFICATION GAP
OPTIONAL / FUTURE
```

Do not resolve an open design question inside the handoff.

### 9. Current evidence / important artifacts

List only materially useful artifacts:

```text
concept files
ChatGPT task(s)
Codex report(s)
important commit(s)/PR(s)/issue(s)
scientific paper DOI/source
external repository + commit/release
important user-provided source filenames
```

Prefer stable identifiers/links over copied content.

### 10. Next actions

Give an executable continuation order and distinguish ChatGPT DIRECT work from genuinely local Codex work. Include `Do not start yet` only when it prevents a likely sequencing error.

### 11. Project-specific User constraints

Record only project-relevant constraints that materially change future decisions or execution. Do not copy global collaboration policy already recoverable from current authority.

### 12. Source pointers / raw provenance

Preserve enough raw provenance to trace the summary back to durable material without copying the full conversation:

```text
source conversation title/time range/URL when available
repository + branch + handoff HEAD
collaboration commit
concept/task/report immutable links
important PR/issue/commit links
paper DOI / stable citation
external repository + revision/release
important user-provided source filenames
previous handoff path
```

A full chat transcript is not required.

## Authoring procedure

When producing a handoff, ChatGPT should:

```text
1. resolve current project/collaboration authority;
2. inspect current repository state + relevant concept/task/report artifacts;
3. summarize the source conversation independently rather than copying long stretches verbatim;
4. distinguish accepted design, implementation state, evidence, and unresolved decisions;
5. create the new handoff;
6. update reports/handoff/README.md current pointer/history;
7. commit/push;
8. give the User the committed path/link and minimal new-conversation start instruction when useful.
```

## Quality check

A fresh Agent should be able to recover:

```text
project objective
current architecture/state
authoritative files
settled decisions + rationale
rejected directions
implemented versus only designed state
unresolved decisions + owners
next actions
underlying evidence pointers
```

If this requires several older handoffs or reconstruction of the source conversation, the new handoff is insufficient.
