id: 042cxmth0
kind: issue
title: Add an offline `qew inbox` for one person: waiting drafts, assigned work, session summary line
parent: 042cxmt4m
needs: 042cxmtgv
labels: area:board-admin
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
evidence: lyzzommk
---
## Behaviour
`qew inbox [--login L] [--count] [--json]` reads only the ledger. Sections: `waiting` (draft items authored by L, i.e. waiting for a human to approve), `assigned` (items currently claimed by L; open, derived from claim events). Replies from forge comments are out of scope until the ledger models comments (list in dropped). `--count` prints one line for the session-start hook and conflicts with `--json` (exit 2); an invalid login is refused (exit 2); login defaults to the configured actor. Titles go through the shared untrusted-text helper. JSON rows carry `schema_version` and `section`. No state is kept.

## Scenarios
- `inbox_lists_waiting_and_assigned_sections`: golden: one draft by L, one claimed by L, one claimed by M; only the first two appear.
- `count_line_is_one_line_and_exclusive_with_json`: both flags: exit 2.
- `invalid_login_is_refused_before_any_read`: prevents a pattern as a login.
- `hostile_titles_are_flattened`: newline title prints on one line.

## Reference coverage
Reference inbox module (replies, waiting, assigned sections, count line, excerpt cap 100, control characters stripped, bot and marker comments excluded); the reference has inbox tests outside this audit's file filter, so no function in the scoped files maps here directly.

## Qew today
Missing. `qew hook session-start` prints ready work only.
