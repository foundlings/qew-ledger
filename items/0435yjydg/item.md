id: 0435yjydg
kind: issue
title: Claim arbiter reported unreachable during qew sync, leaving claims provisional
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-22T15:07:53Z
discovered_from: 0435ydxgy
evidence: tlkuusnyxtsq owpnympsyrkm
---
## Problem

On foundlings 2026-10-22 qew sync reported 'claim provisional: ... the arbiter is unreachable' and left claims 042p5dc2v and 0431hi70e provisional, and the sync took minutes waiting on it. Cause not yet known.

## Fix

Find why the arbiter looked unreachable (timeout, fetch/merge path, remote lock), make sync settle claims against the ledger remote it just fetched, and fail or retry with a clear reason.
