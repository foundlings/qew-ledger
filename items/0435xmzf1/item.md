id: 0435xmzf1
kind: issue
title: qew pull: fetch-only ledger update, and reads fetch on a miss
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-22T14:48:39Z
---
## Problem

After another machine lands work, the only way to see it is qew sync (full forge reconcile, arbiter round-trip, minutes on 2133 items). qew show says 'no item matches' and qew pr merge says 'pull request is not recorded in the ledger' until then; reads fetch at most every fetch_interval_s.

## Fix

Add qew pull: forced ledger fetch+merge only, no forge reconcile and no worker, reports the new head and changed items, fails fast on conflict or unreachable remote. An item or pull request miss in a read or pr command pulls once and retries before refusing.
