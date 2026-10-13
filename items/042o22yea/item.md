id: 042o22yea
kind: issue
title: qew batch --manifest: many mutations under one lock, one snapshot and one commit
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-13T17:57:08Z
---
Santa: on a 22.8k-item ledger one mutation holds the write lock 13-20 s (full snapshot 5-8 s, jj snapshot+commit 5 s, resolve 1-4 s), so 900-row reconciles take hours. Add qew batch --manifest FILE with op rows (start, evidence, complete, close, reopen, set, comment), validated and applied all-or-nothing in one session, reusing one snapshot across rows.
