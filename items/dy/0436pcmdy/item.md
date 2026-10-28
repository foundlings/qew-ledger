id: 0436pcmdy
kind: issue
title: qew push --item with several items can leave unpushed above 0 until a second push
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-22T23:54:26Z
discovered_from: 0436obtee
evidence: 23ad4abe928786a739fc5b18aa416fc16044b9b0
---
## Goal

After a multi-item qew push --item the ledger remote should be caught up (unpushed=0) without a second push. Seen by wolf on 6.36.2: a second push said nothing pending and then status showed unpushed=0; likely the mirror-record commit lands after the ledger push. Reproduce with a multi-item push against a ledger remote, assert unpushed=0 after one push.
