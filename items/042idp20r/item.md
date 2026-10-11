id: 042idp20r
kind: issue
title: A large attachment is never committed on a jj ledger: jj refuses to snapshot a new file over snapshot.max-new-file-size, and check does not see it
parent: 
needs: 
labels: 
owner: 
priority: 1
created: 2026-10-11T10:21:07Z
---
Foundlings: items/042fi53dn/attachments/afea62....json is 6.1 MiB, dated Oct 10 20:12, untracked in the canonical checkout, never pushed; jj prints the warning on every command. qew's attachment limit is 100 MiB. Fix: qew's jj commands pass --config snapshot.max-new-file-size above that limit so qew-owned files always snapshot; recovery commits a stray one on the next write; qew check reports an attachment file that is not in the committed tree.
