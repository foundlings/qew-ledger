id: 044qpfm4u
kind: issue
title: test_background_sync_walk test_concurrent_writes_never_double_sync flakes: an id left queued / 5 of 6 items synced
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-11-18T19:03:41Z
---
## Problem

Fails about 1 run in 3 solo and sometimes in the parallel gate (seen before the 7.0 changes): 'an id was left queued' or '5 of 6 items synced'.

## Done when

20 consecutive solo runs pass, or the race is found and fixed
