id: 042cxmtgr
kind: issue
title: Give `qew check` a stable machine report with canonical cycles and state contradictions
parent: 042cxmt4m
needs: 042cxmtgq
labels: area:board-admin
owner: 
priority: 3
created: 2026-10-08T17:20:13Z
---
## Behaviour
`qew check --json` prints one object: `schema_version`, `valid`, `cycles` (each cycle listed once, rotated so its smallest id comes first and closed back on it, list sorted), `contradictions` and `text_findings`. Contradictions that remain representable in the ledger: a claimed epic (epics are never claimed), a child of a completed epic that is not done, a completed item with open needs. Multiple priorities or kinds are unrepresentable in the header and need no check. Writes nothing.

## Scenarios
- `cycles_are_reported_once_in_canonical_rotation`: a three-item cycle entered from any node prints identically; prevents unstable diffs.
- `claimed_epic_is_a_contradiction`: an epic with a claimed event is reported by id; prevents a state the board cannot show.
- `valid_ledger_reports_valid_true_and_exit_0`: empty lists, schema_version present.

## Reference coverage
No test file of its own in the reference; the diagnostics module backs the graph report used by the read suite (read-suite tests belong to another audit). Covered text part sits in `output-untrusted-text`.

## Qew today
Reduced: `ledger_check.check` finds cycles, dangling needs, illegal transitions (tests/test_check_walk.py, 7 tests) but prints plain problem lines only.
