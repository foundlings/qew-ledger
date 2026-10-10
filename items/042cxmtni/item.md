id: 042cxmtni
kind: issue
title: Make inbox refuse malformed or inconsistent event data
parent: 042cxmtmt
needs: 042cxmtnf
labels: area:read-side
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
## Behaviour
An unparseable comment time, a comment without a body, an item without a title, or an event stream that cannot be read to the window start fails the inbox with exit 1 and empty stdout. The ledger has no search paging, so the reference paging adversaries (label churn burying a reply, older comment pages hidden behind a last-N cut, missing cursor) reduce to one rule: the inbox scans every event of every candidate item, never a tail slice.

## Scenarios
- refusal: each of four corrupt shapes (bad time, missing body, missing title, truncated event file) fails with empty stdout and a reason. Prevents a quiet partial inbox.
- adversary: an item with 2000 events where the only in-window reply is the 1500th is still found. Prevents a bounded tail scan hiding a reply.

## Reference coverage
Reference inbox walks: truncated or malformed API data fails loudly; unreachable older comments fail loudly; search paged to the end; older comment pages fetched until window is covered (4 tests, forge cursor mechanics dropped, behaviour kept).

## Qew today
Missing.
