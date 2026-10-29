id: 042cxmtke
kind: issue
title: Give `qew reopen` a reason and make reopening an open item a no-op
parent: 042cxmtjw
needs: 
labels: area:lifecycle
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
evidence: lyrtzqmu
---
## Behaviour
`qew reopen ITEM --reason TEXT` records why work is required again on the `reopened` event; the fold already clears the owner so no stale claim survives. Reopening an item that is already open (draft, approved, claimed) is a write-free no-op, exit 0, output `unchanged ITEM (already open)` (reference), instead of today's exit 2 refusal; a completed item that other completed items depend on reopens and its dependents become blocked again (derived). Reopen returns to approved, never to claimed.

## Scenarios
- golden: closed item with a stale claim reopens as approved, owner empty, reason recorded, item back in `qew ready` (covered for ready by flow walk test_release_close_and_reopen; reason missing)
- reopen an open item: exit 0, no event written (prevents: duplicate events from idempotent loops)
- reopen a completed dependency: dependents show up in `qew blocked` again (prevents: stale readiness)

## Reference coverage
2 reference test function(s): `test_reopen_golden_walk_releases_every_stale_claim`, `test_reopen_open_issue_is_a_write_free_noop`

## Qew today
Reduced. Reopen exists and is covered by test_release_close_and_reopen; no reason, and an open item is refused with exit 2.
