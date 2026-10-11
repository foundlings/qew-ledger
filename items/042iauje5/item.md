id: 042iauje5
kind: issue
title: A local SQLite cache of the ledger's files, validated by stat, makes every command's whole-ledger read cheap
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-11T09:23:04Z
---
Foundlings: a snapshot reads 165k files and takes 17-27 s. Cache raw item and event texts in .qew/snapshot.db; re-read only entries whose stat signature changed. Design measured in the session; target up to 500k files.
