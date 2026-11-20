id: 044up4t7x
kind: issue
title: A second completed event on a completed item made the whole ledger unreadable: the fold tolerates the duplicate; find how it was written
parent: 
needs: 
labels: 
owner: 
priority: 0
created: 2026-11-20T18:35:43Z
---
## Problem

Santa 2026-11-20: events/044tp182k holds 044uon3g8 and 044uoni4s, both completed by 887 15s apart (two repair-evidence events with ssh and https repo urls); every read failed with completed is illegal from state completed.

## Done when

A duplicate completed of a completed item reads as one completion (fleet unblocked); the writer path that appended the second is found and refused without writing.
