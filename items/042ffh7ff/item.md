id: 042ffh7ff
kind: issue
title: Bulk comments for importers: manifest and create --from-file
parent: 042ffd5dc
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-09T23:14:12Z
---
qew comment --manifest FILE (JSON Lines: item, text, author, at, reply_to, key) and comments inside create --from-file plan lines, applied in ONE commit, idempotent by key, with the original author and time preserved as provenance import. Walk: 500 comments across 40 items in one commit, rerun is a no-op.
