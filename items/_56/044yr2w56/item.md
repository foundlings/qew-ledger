id: 044yr2w56
kind: issue
title: A write verb under the ledger lock parses only what it needs
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-11-22T18:53:46Z
---
## Problem

start, evidence and complete parse the whole ledger (4 to 5 s on foundlings) inside the write lock, so fifteen writers queue for minutes.

## Approach

Measure each write verb on a clone of the foundlings ledger, then serve the parse from the warm snapshot or load only the items the verb touches.

## Done when

each write verb's time under the lock is measured before and after on the clone, and the slowest is cut
