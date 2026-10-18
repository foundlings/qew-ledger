id: 042y7ue3h
kind: issue
title: A fresh checkout counts every mirrored item as a pending update
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-18T19:00:29Z
---
On a second machine the committed mirror files name every issue but the local sync state (synced_event, synced_hash) is never committed, so qew status shows pending=N for every item and a plain qew sync is refused by sync_limit, though no item needs a forge write. The pull already baselines first contact without pushing. Count those items as unbaselined, not pending, keep them out of the sync_limit count, and record the newest event when baselining so the first sync clears the count.
