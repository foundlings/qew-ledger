id: 043isee2d
kind: issue
title: migrate-layout: shard directories named _xx so they cannot collide with item ids; rollback restores the exact tree; resumable; structural check; --no-check
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-28T23:51:44Z
---
## Goal

a failed or interrupted migration leaves the pre-migration tree (empty git status), a rerun finishes it, and the check afterwards ignores uncommitted attachments
