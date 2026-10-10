id: 042geqx0k
kind: issue
title: Sync settles divergences by itself: the ledger wins unless the mirror is set to report
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-10T10:53:27Z
---
Owner: 'you should auto fix divergences!! argh!'. A forge-side change the ledger did not make (a human closing or editing a mirrored issue) is a forge_divergence that waited for qew accept/reject forever. New [replication] divergences = "ledger" (default) | "report": with ledger, sync rejects each open divergence right after the pull (the ledger is the source of truth), so the same sync pushes the ledger value back and records divergence_rejected with the reason auto; contested claims stay arbitrated as before. report keeps the old behavior.
