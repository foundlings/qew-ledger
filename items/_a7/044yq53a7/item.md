id: 044yq53a7
kind: issue
title: Serve reads from a warm parsed snapshot instead of parsing the whole ledger
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-11-22T18:34:38Z
---
## Problem

Every read command (show, list, ready, progress) parses all items and events of the ledger: about 5 s of CPU on foundlings (28k items, 220k events), multiplied by about 15 agents reading at once.

## Approach

Keep the parsed snapshot in .qew beside snapshot.db, valid while the ledger generation (bumped by every qew write and pull), the ledger git head and a max age are unchanged; a restricted unpickle; a clean full parse stays the fallback and the qew check path.

## Done when

a second read of an unchanged ledger skips the parse, every write invalidates it, a damaged or unknown warm file is ignored, QEW_NO_CACHE bypasses it, and qew check still parses everything
