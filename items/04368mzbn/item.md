id: 04368mzbn
kind: issue
title: A targeted qew push/sync --item settles every open divergence of the target, one full ledger snapshot each, and stalls on a big ledger
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-22T18:33:14Z
---
## Problem

settle_automatically rejects every open divergence of the target through reject(), which rebuilds the whole snapshot per divergence (2.6s on foundlings' 23k items); a push of one item with many open divergences runs for minutes (wolf: 25 snapshots in 90s, recover 69 files)

## Done when

settling reads the ledger once for all divergences, and a targeted pass settles only the touched items' divergences; a push of one item is not slowed by divergences on other items
