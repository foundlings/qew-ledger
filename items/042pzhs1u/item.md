id: 042pzhs1u
kind: issue
title: qew sync is scoped: --all, --since, --author, --owner, --tree, --limit; a large unscoped sync is refused
parent: 
needs: 
labels: 
owner: 
priority: 1
created: 2026-10-14T16:53:42Z
evidence: yrytsntxkrku umsqwwqourto
---
## Problem

qew sync pushes every selected item to every mirror. On a big ledger the first sync, or a schema change, writes thousands of issues and cards at once, runs into forge limits and gets stuck.

## Fix

sync gains --since DATE, --author NAME, --owner NAME, --tree ITEM and --limit N (intersecting, parents first); they use the targeted pass, which reads no whole board and prunes nothing. An unscoped sync whose pending writes exceed [replication] sync_limit (default 300) is refused with the count and the options unless --all is given. The background worker syncs its queued items and logs the refusal.

## Done when

Each filter narrows the writes; an over-limit sync without --all exits 2 naming the count and --all; --all and --dry-run still work; the worker keeps mirroring queued items.
