id: 042fee6bs
kind: issue
title: Rename the time id mode to base35-time
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-09T22:52:01Z
---
Owner 2026-10-10: 'time' is a terrible name for the base-35 time string; call the mode base35-time (id_mode, qew migrate-ids --to base35-time, docs, init template). Strict rename, no alias: the owner says no consumer depends on it yet. foundlings' qew-ledger.toml uses id_mode.issue/task = time and must change to base35-time together with the version that carries the rename (minimum_version). Event IDs keep their own description (always time-ordered).
