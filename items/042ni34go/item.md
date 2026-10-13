id: 042ni34go
kind: issue
title: Board cards of closed stray issues stay in In progress and project status reports in sync
parent: 
needs: 
labels: 
owner: 
priority: 1
created: 2026-10-13T11:29:19Z
---
## Problem

foundlings/qew #484 and #485 were closed by qew mirror rehome but their cards stayed In progress on the shared board; project status ignores cards the ledger does not mirror and there is no way to remove them (prune refuses the board's own repo).

## Done when

project status reports orphan cards of the board's own repository; project prune --orphans removes them and verifies; rehome tells where the card goes.
