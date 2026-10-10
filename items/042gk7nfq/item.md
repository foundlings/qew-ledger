id: 042gk7nfq
kind: issue
title: Evidence resolution is fast on a big checkout: batched, read-only jj and git calls
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-10T12:45:17Z
---
Santa: migrate-layout dry-run on foundlings ran 40+ minutes: one jj log per cited id, each snapshotting a 60k-file working copy. Fix: every resolution jj call is read-only (--ignore-working-copy --no-pager); a manifest or check or migration resolves all ids in a few calls (ancestors of the target once, a batched change_id revset for the rest, git rev-list + cat-file --batch-check). Applies to migrate-layout, check, evidence --manifest and complete.
