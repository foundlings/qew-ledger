id: 043f859e0
kind: issue
title: qew check reports a write in flight (event before its item) as ledger problems and sync refuses
parent: 
needs: 
labels: 
owner: 
priority: 1
created: 2026-10-27T05:34:44Z
discovered_from: 043f66nch
---
## Goal

qew check reads without the ledger lock, so a concurrent writer or checkout shows as 'events/ID: belongs to no item' or 'synced_event newer than the item's newest event', and qew sync then stops with 'the ledger has N problem(s)'. Reported on foundlings (Santa, Rudolph, 3 orphan events that were gone on the next look). Re-scan while another process holds the write lock, bounded, without taking the lock.

## Done when

A walk shows a transient orphan event is not reported once the writer finishes; a persistent one still is, after at most the bound; with no writer, or the checking process itself holding the lock, a problem is reported at once; no lock is taken so nothing can deadlock; specs agree; gate green.
