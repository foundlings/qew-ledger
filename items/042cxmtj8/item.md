id: 042cxmtj8
kind: issue
title: Give `qew hook install|remove` a versioned machine-readable result
parent: 042cxmtj6
needs: 
labels: area:hooks-dist
owner: 
priority: 3
created: 2026-10-08T17:20:13Z
evidence: rtlnrlyw
---
## Behaviour
`qew hook install|remove --json` prints a stable object per agent: action (`installed|removed|unchanged`), agent, `schema_version`, and `trust_required` for Codex. With several agents the object carries an `agents` list in the fixed order claude, codex, cursor, opencode. Human output stays one line per agent, with the Codex trust line `review and trust it with /hooks before it will run`.

## Scenarios
- Single agent `--json` on a fresh checkout: exact object incl. `trust_required: true` for Codex. Prevents scripted setup guessing whether a manual trust step remains.
- All agents `--json` after an install: every entry `unchanged`, order fixed. Prevents non-idempotent reruns being invisible to automation.

## Reference coverage
2 tests (codex versioned machine output; the JSON half of install-all).

## Qew today
Missing. `cmd_hook` prints human lines (the trust line exists) but the command has no `--json`, and no test pins the human trust line either.
