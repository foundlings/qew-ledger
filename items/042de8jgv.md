id: 042de8jgv
kind: issue
title: Warn when a created or edited body holds unmarked code-shaped text
parent: 
needs: 
labels: area:read-side
owner: 
priority: 2
created: 2026-10-08T22:59:34Z
---
<!-- qew-duplicate -->

## Behaviour
When `qew create` or `qew set --body` is given Markdown prose, a high-precision detector reports tokens that look like commands or paths but are not inside backticks or fenced blocks: long flags (`--name`), absolute or dot paths, `qew ...` subcommands, `git`, `gh`, `python -m` and `pipx` invocations. Each prints `warning: unmarked code-shaped text: TOKEN` to stderr, deduplicated and in order of appearance; the write still succeeds (advisory). Fence handling accepts three-backtick and tilde fences, ignores indentation, and treats an unclosed fence as code to the end. Purpose: agents quoting commands unmarked in an item body makes later readers (and agents) treat them as instructions.

## Scenarios
- golden: a body with `run qew start X --force` unmarked warns for the command and the flag; the same text in backticks or a fence warns nothing. Prevents instruction-looking prose in bodies.
- adversary: a fence opened with tildes and an unclosed fence hide their content; a path glued to a colon (URL) is not reported. Prevents false positives on URLs and false negatives after odd fences.
- golden: write succeeds and exit code is 0 even with warnings. Prevents the advisory becoming a blocker.

## Reference coverage
Reference code-prose module used by body-writing commands; no dedicated test file in this area (behaviour checked indirectly by command walks owned by other areas).

## Qew today
Missing.

---
042cxmtnj · approved · issue
Parent: #202
