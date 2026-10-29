id: 042cxmtgi
kind: issue
title: Verify board placements by re-reading with bounded retries and fail closed
parent: 042cxmt4m
needs: 042cxmtgf
labels: area:board-admin
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
evidence: pwpxwtor
---
## Behaviour
After `qew sync` or `qew project ensure` places cards, re-read the board and compare each placed card's column/priority with what was written. Eventual consistency is tolerated: retry mismatching reads a fixed small number of times (reference: 5 retries over about 20 seconds, scaled down by an environment variable for tests) and print one stderr warning per failed attempt 'board verification attempt 3/6 failed: item X; retrying'. A malformed read fails immediately. A persistent mismatch names each missing item/field, prints nothing on stdout, and exits non-zero (3 = verification failure) WITHOUT recording the mirror column (so the next sync repairs it). Only mismatched reads are retried, never the writes.

## Scenarios
- `delayed_card_visibility_is_retried_then_succeeds`: card invisible for two reads then present: success with an attempt warning on stderr; prevents false failures from lag.
- `permanent_mismatch_fails_closed_and_names_the_item`: never-visible card: exit 3, stdout empty, stderr names the item, mirror column not recorded; prevents reporting success for a lost write.
- `malformed_board_read_is_not_retried`: garbage payload is a typed error on the first attempt; prevents masking a protocol bug.

## Reference coverage
Tests: ensure retries delayed item visibility (call count and warning text), ensure reports a permanent verification mismatch (exit 3, empty stdout, named item). Spec: reconciliation cost section.

## Qew today
Missing. `sync._place` records `column` in the mirror file as soon as `place_on_board` returns; nothing reads back, so a lost write is remembered as done and never retried.
