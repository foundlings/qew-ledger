id: 042d0fgf5
kind: issue
title: Drive finding: two checkouts syncing the same forge target can create duplicate issues
parent: 
needs: 
labels: drive-finding area:replication
owner: 
priority: 0
created: 2026-10-08T18:17:46Z
---
Seen live: several checkouts each run a background worker against foundlings/qew at once; each has its own sync lock, so two workers can both miss the marker and both create the issue for one item.

Fix options to decide in the issue: (1) after a create, list issues by marker and, if a lower-numbered issue carries the same marker, adopt it and close ours as duplicate with a comment; (2) a per-target sync lease recorded on the forge or the ledger remote. Either must be idempotent and tested with two concurrent workers against the Forgejo and GitHub fakes.

Scenario: two concurrent syncs of one new item end with exactly one open issue and one mirror.
