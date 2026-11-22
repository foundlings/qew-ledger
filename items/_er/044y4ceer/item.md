id: 044y4ceer
kind: issue
title: qew sync is O(all): full issue pull exceeds the 50-page cap and fails after doing all the work
parent: 
needs: 
labels: 
owner: 
priority: 0
created: 2026-11-22T11:30:09Z
evidence: knvnqwoy xrkvlnzy upqquwnw svlotzlq nksxpktl twsnxtsx
---
## Where

src/qew/forge_pull.py, sync.py, forge github listing, snapshot.db/remote-state

## Problem

Foundlings (5000+ issues): a no-change qew sync runs 3+ minutes at 80% CPU, walks the whole ledger (unchanged 2570), then fails with 'pull failed HTTP 200: more than 50 issue pages; refusing a truncated listing', so it repeats every time. Also repeats 'warning ACQ: priority 5 shown as P4' and 'WP-ACQ-01' each full sync. A ledger write must never wait on a GitHub pull.

## Fix

Incremental pull: GitHub since=<last remote-state timestamp> and/or ETag If-None-Match, so a no-change sync costs one or two requests; O(changed) pass off snapshot.db; keep the truncation refusal but never need more pages; dedupe repeated warnings; check sync.spawned and sync.queue do not block writes.

## Done when

A walk with a large fake forge shows a no-change sync makes at most a few requests and no full walk, a changed issue is still picked up, and a 60-page listing is not needed.
