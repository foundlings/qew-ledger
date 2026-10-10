id: 042cxmtkr
kind: issue
title: Give every write command a versioned `--json` result
parent: 042cxmtjw
needs: 
labels: area:lifecycle
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
## Behaviour
Agent loops parse results, not prose. Reference write commands accept `--json`, also placed before the command, and print an object with `schema_version`, the item id and the new state: create (`{id, state, schema_version}` per item), set (`changed`), start (`state: started`, plus `lane`, `workspace`, `kind` when given), complete, close, reopen, release, block, unblock, land. Human output stays one terse line. Pin each schema in a test, and list it in docs/specs/commands.md. The reference's stderr reconciliation hint for boards is dropped (the ledger is the board source).

## Scenarios
- start with the flag before the command and after it: identical JSON with `schema_version` 1 (prevents: agents guessing flag position)
- create json for a batch returns an array in input order with ids and states (prevents: parsing stdout lines)
- error paths keep the plain stderr message and exit code (prevents: JSON mode hiding failures)

## Reference coverage
2 reference test function(s): `test_global_machine_flags_render_versioned_lifecycle_json`, `test_json_create_also_names_the_reconciliation_command_on_stderr`

## Qew today
Reduced. `--json` exists on show, list, ready, blocked and graph only; write commands print prose.
