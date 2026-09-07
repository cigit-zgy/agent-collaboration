# Copyable Codex launch prompt

## Decision

FORMAL ChatGPT → Codex launch prompts are user copy/paste controls, not prose quotations.

The user-visible Codex launch prompt MUST be rendered as a Markdown fenced code block with opening fence exactly:

````text
```text
````

and a three-backtick closing fence.

Markdown blockquotes, callouts, writing blocks, lists, inline code, or ordinary paragraphs are not conforming launch surfaces because they do not reliably provide the direct Copy interaction expected by the User.

## Rationale

The User routinely launches local Codex tasks from ChatGPT, often from mobile. The launch text is intentionally short and should be transferable with one Copy action. The durable task file remains the task-specific authority; the code block is only the locator/launcher.

## Boundary

This decision changes presentation, not task semantics.

The authoritative operational owner is:

```text
references/collaboration/templates/chatgpt-task.md
```

The launch block continues to contain only repository/task/branch/commit/collaboration coordinates, immutable task URL, and the authority sentence. Detailed task requirements remain in the committed task artifact.
