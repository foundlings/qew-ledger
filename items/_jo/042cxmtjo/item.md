id: 042cxmtjo
kind: issue
title: List subcommands of every command group with a help line and keep gates strict
parent: 042cxmtj6
needs: 
labels: area:hooks-dist
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
evidence: wysxusny
---
## Behaviour
`qew --help` has a workflow-grouped epilog (Read, Work, Drafts, Pull requests, Mirrors, Setup) containing every top-level command and points at `qew COMMAND --help` and the drafts flow (`qew draft approve|revert`). Each group command (`draft`, `pr`, `hook`, `project`, `sync`, ...) lists all its subcommands, each with a help line. Every option and argument has help.

## Scenarios
- Epilog lists every top-level command under a group and names the draft approve/revert verbs (group coverage exists; the pointer text is untested). Prevents a command nobody can discover.
- For each group command, `--help` shows every subcommand with a non-empty help line (current gate walks the parser, not the rendered text). Prevents invisible subcommands in the rendered output.
- Every flag has help (covered) and every `--flag` appears in README and docs/specs/commands.md (covered).
- A new command in no group fails (covered).

## Reference coverage
6 tests (every command in a group; help points at per-command help; subcommand groups list subcommands; every top-level has a help line; every option documented; flags in README and spec).

## Qew today
Mostly covered by 4 help walks including a section-sign gate. Missing: the rendered per-group help check and the pointer text.
