id: 042fksf96
kind: issue
title: A sync whose last mirror writes were checkpointed leaves its ledger commit unpushed
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-10T01:02:15Z
evidence: qkwrzontpxvo rnwxntqyvmnk
---
Santa 2026-10-10 (foundlings): after the PIE rename the first qew sync ended with unpushed=1 and needed a second sync. Cause: replication.checkpoint commits the mirror files every 25 writes without pushing; the session end commits and pushes only when entries remain, so a sync whose writes were all checkpointed pushes nothing. Fix: remember that a checkpoint committed and push at the end of the session.
