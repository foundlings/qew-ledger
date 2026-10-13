id: 042o4pz4q
kind: issue
title: batch --dry-run and a failing batch leave start claims on the primary forge; release --force cannot clear them
parent: 
needs: 
labels: 
owner: 
priority: 0
created: 2026-10-13T18:50:49Z
---
Santa (foundlings): a dry run of start rows left 20 claims on the primary that nothing in the ledger holds; start then refuses 'already claimed by X on the primary' and release/take-over say not claimed. Rollback only undoes ledger files. Fix: dry run never writes the primary; a failing batch withdraws what it posted; release --force clears a primary claim the ledger does not hold.
