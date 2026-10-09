id: 042ffeogw
kind: issue
title: Bulk attach for importers: a manifest and attachments in create --from-file
parent: 042ffd5dc
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-09T23:12:43Z
---
qew attach --manifest FILE (JSON Lines: item, source path, name, optional media type) applying many attachments in ONE commit, and create --from-file plan lines accepting an attachments list; idempotent by content hash (a rerun adds nothing), dry-run, per-file and total limits enforced, a failure leaves nothing partial. Walk: 300 files across 40 items in one commit, rerun is a no-op.
