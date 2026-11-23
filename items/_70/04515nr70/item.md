id: 04515nr70
kind: issue
title: A scoped qew push created three forge issues and none was recorded as a mirror on the pusher's checkout
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-11-23T23:40:21Z
---
## Where

src/qew/sync.py _sync_item, replication.py _commit/push

## Problem

Wolf's three 'qew push --item 045151p7h' on 7.2.12 each exited 0 ('pushed 1 item') and each created a forge issue (#8546, #8549, #8551), yet pull and show saw no mirror and --dry-run still said create. A later sync (c19328a33e) recorded #8546 on the ledger remote; qew's duplicate guard had already closed #8549 and #8551. The mirror write after the create did not reach the remote from the pusher's checkout.

## Fix

Find where the mirror commit or its push is lost (unpushed local commit, a merge that took the other side, a rollback); a scoped push must never create twice: the second push must find the first's issue by its marker before it creates

## Done when

A walk reproduces a pusher whose mirror commit does not reach the remote and shows the next push adopts the existing issue instead of creating another
