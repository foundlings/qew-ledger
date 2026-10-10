id: 042d0iza9
kind: issue
title: Drive finding: mirror files rewritten by several checkouts produce real merge conflicts; split identity (shared) from sync state (local)
parent: 
needs: 
labels: drive-finding area:replication
owner: 
priority: 0
created: 2026-10-08T18:19:49Z
evidence: mzyzmozu
---
Seen live: after three scratch checkouts and the shared checkout synced foundlings/qew, the shared ledger's main bookmark was conflicted (mirrors/<ID>/<target>.json 2-sided conflict) and pushes were refused. Cause: every sync rewrote the mirror file (synced_at, synced_event, synced_hash, seen, linked, column), so two machines edit the same file.

Fix: a mirror file in the ledger holds only the immutable identity (forge, url, kind, number, node_id, issue_url, head) and is written once; volatile sync state (synced_*, seen, linked, column) moves to the local cache `.qew/state/<target>/<ITEM>.json` (never committed). Readers merge both (old mirror files with volatile keys still read). Pending becomes per-machine knowledge.

Scenarios: two checkouts syncing one target and editing the same items merge without conflicts; the committed mirror file never changes after creation; an old-format mirror file still reads; status/pending use the local state.
