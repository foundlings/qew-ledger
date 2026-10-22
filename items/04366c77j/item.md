id: 04366c77j
kind: issue
title: qew push sends pending changes to the forge; a bare qew sync is refused with exit 2
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-22T17:46:42Z
---
## Problem

qew sync is the only way to send ledger changes to the forge, and a bare call reads the whole board, merges, pushes and prints a lot: an agent that wanted to push one close pays for all of it, and a human closing an issue by hand still needs a full sync

## Done when

qew push writes only pending items (targeted read, no whole-board listing, no pruning) and prints one line; a bare qew sync exits 2 naming push, pull and the options; any option keeps today's sync; the background worker is unaffected
