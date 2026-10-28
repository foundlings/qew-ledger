id: 043ihfagn
kind: issue
title: shard events, items, mirrors and baselines by id suffix so a commit rewrites a small tree (schema 8 and a rename migration)
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-28T20:28:05Z
evidence: e596f481 83200ab3
---
## Goal

events/<xx>/<item>/ and the other owned directories hold ~20 entries per shard; one id-to-path function; a migration commits the rename once; commit cost no longer scales with ledger size
