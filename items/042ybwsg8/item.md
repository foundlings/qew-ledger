id: 042ybwsg8
kind: issue
title: Commit the forge-synced baseline per item so a clone starts from it
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-18T20:23:32Z
---
The sync baseline (hash, newest synced event, what the forge showed) lived in uncommitted .qew/state, so every clone started from nothing. Commit it as baselines/ID/TARGET/ID2.json, one live file per item and target, replaced by a new file on change so two machines never write the same path. A machine's pending changes stay derived from events newer than the baseline.
