id: 042cxmtiu
kind: issue
title: Compose structured work bodies and warn about unmarked code text
parent: 042cxmti7
needs: 
labels: area:drafts-plans
owner: 
priority: 3
created: 2026-10-08T17:20:13Z
---
## Behaviour
Reference `create` and plan lines build the body from `where`, `problem`/`goal`, `fix`/`approach`, `done-when`,
`discovered-from`, with an ambiguity refusal when both `problem` and `goal` (or `fix` and `approach`) are given, an
`--edit` flow that runs `$EDITOR` without a shell, and warnings for unmarked code-shaped text. This is optional
authoring convenience; confirm there is a current requirement before building (YAGNI). If built in the ledger
model: sections render as plain Markdown headings in the body; `done-when` entries become child `task` items
(the spec forbids inline checkboxes); `discovered-from` becomes a `needs`-free provenance line naming the item;
`$EDITOR` is split with shlex and executed without a shell; warnings go to stderr and never alter the body.

## Scenarios
1. Composed body: goal, approach and done-when produce the headings and child tasks; `discovered-from` line present. Prevents free-form, unreadable work text.
2. `--problem` with `--goal` refused exit 2, no call. Prevents two framings of one item.
3. `EDITOR="python editor.py ; touch marker"`: marker is never created and the edited text becomes the body. Prevents shell injection from an environment value.
4. Body mentioning `qew ready --limit 5` and `./plans/work.jsonl` produces stderr warnings and an unchanged stored body. Prevents untrusted text being silently turned into commands.

## Reference coverage
Reference graph-write: create golden walk composes approved work, create seam walk refuses ambiguous body, create editor
golden walk uses editor body without a shell, create warns about unmarked code without altering the body (4 of 26).

## Qew today
Missing: `create` has `--body`/`--body-file` only; no structured fields, no editor, no warnings.
