id: 042yejkcq
kind: issue
title: Declare schema 7 for the committed baselines layout so an older qew refuses the ledger
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-18T21:17:40Z
evidence: toklnpqsyxpn orxqlrrqqkkt
---
baselines/ID/TARGET/ID2.json is a new ledger layout. A qew older than 6.31 ignores it and keeps its sync state local, so it must not work on such a ledger. Bump CURRENT_SCHEMA to 7 (qew init writes it, qew migrate-layout moves 6 to 7 by declaring it), so older qews fail with 'schema_version 7 is not supported; upgrade qew'.
