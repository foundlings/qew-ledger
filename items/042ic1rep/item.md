id: 042ic1rep
kind: issue
title: A read on a large jj ledger snapshots the working copy a dozen times: fetch, queries and recovery scan 165k files
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-11T09:47:41Z
---
Santa: warm reads 15-19 s on the live loaded ledger with 8 s in ledger fetch+merge and sys time 37-56 s. jj commands without --ignore-working-copy snapshot every time.
