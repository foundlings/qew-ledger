id: 043iy5j4e
kind: issue
title: the background sync queue loses ids: an append to sync.queue racing the worker's take is deleted with the renamed file
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-29T01:49:04Z
evidence: e5b2bae4 28119b57
---
## Goal

enqueue and take_queue are serialised by a lock, so no id a write queued is ever lost; a lock timeout falls back to the full catch-up pass
