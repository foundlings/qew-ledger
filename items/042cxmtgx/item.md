id: 042cxmtgx
kind: issue
title: Version-gate and harden the config contract: minimum_version, schema strictness, tracked policy
parent: 042cxmt4m
needs: 
labels: area:board-admin
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
## Behaviour
`.qew/config.toml` accepts an optional `minimum_version = "MAJOR.MINOR.PATCH"` under `[qew]`. A qew older than it refuses EVERY command before any work (exit 2) naming the required and running versions and the upgrade script (`scripts/setup_user.py`). Equal or lower minimums pass; malformed values (`1.x`, `1.2`, `v1.2.3`, `1.2.3-rc1`, a number) are refused before any call. Unknown top-level keys and unknown mirror options are ignored (additive fields must not break older qew), while `schema_version` in `qew-ledger.toml` stays strict: an unsupported value is refused loudly and a missing one is read as 1. A symlinked config is refused. Qew's own repository tracks its config and a test asserts that it names qew's board and minimum version (the dogfood policy), so a change cannot unlink the board unnoticed.

## Scenarios
- `unknown_config_fields_are_ignored`: future key and future mirror option: commands still succeed; prevents every older qew failing.
- `older_qew_than_the_minimum_is_refused_before_any_call`: message names both versions and the setup script; no forge call, no ledger read.
- `current_and_lower_minimums_are_accepted`: boundary test.
- `malformed_minimum_versions_are_refused`: table of five values.
- `unsupported_ledger_schema_version_is_refused`: schema_version = 2 refused; prevents a silent misread of newer files.
- `tracked_repository_config_links_its_own_board`: the repository's own config pins the board and minimum version; prevents card staleness for qew's own work.

## Reference coverage
Tests: config walk (6: unknown fields ignored, older than minimum refused before any call, current and older accepted, malformed minimum refused, init preserves fields it does not own, mode and schema_version strict), repository config walk (1: tracked config links its own board and minimum version). The mode check is dropped (no mode field).

## Qew today
Missing. `ledger_config.load` has no minimum_version or schema check; mirror unknown options are carried through `options` (partial). No tests of config shape beyond hook tests.
