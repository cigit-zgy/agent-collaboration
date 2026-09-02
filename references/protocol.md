# Collaboration protocol

## Roles

### User

- defines the goal;
- makes scientific and product decisions;
- resolves genuine human-only ambiguity;
- approves exceptional scope changes.

### ChatGPT

ChatGPT is the planner, formal task author, independent auditor, and acceptance
authority. Before writing a task, it inspects the target repository and current
evidence. It commits and pushes the formal task, then gives the User only the
short Codex launch prompt.

After Codex finishes, ChatGPT independently checks the repository, diff,
implementation, report, verification evidence, and relevant artifacts. It does
not accept Codex's self-reported PASS. ChatGPT decides `PASS`,
`PASS WITH LIMITATIONS`, `BLOCKED`, or `FAIL`, and only then decides whether to
open the next task.

### Codex

Codex is the implementer. It executes the committed formal task rather than
guessing requirements from chat. It does not expand scope without approval. It
implements, runs the specified verification, writes the Agent report, commits,
and pushes. Codex does not grant final acceptance.

## Standard loop

```text
User requirement
→ ChatGPT independent inspection
→ ChatGPT formal committed task
→ short Codex launch prompt
→ Codex implementation
→ Codex verification
→ Codex report + commit/push
→ ChatGPT independent audit
→ verdict
→ only then next task
```

## Invariants

- One formal task is active at a time.
- The next formal task starts only after independent audit of the previous task.
- Codex implements; ChatGPT accepts.
- Evidence, not self-reported PASS, determines completion.
- Scientific and product rigor is mandatory; engineering ceremony is not.
