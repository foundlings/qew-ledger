id: 042nejsgg
kind: issue
title: An epic can sit under an epic (nested epics), mirrored as sub-issues, with rolled-up progress
parent: 
needs: 
labels: 
owner: 
priority: 1
created: 2026-10-13T10:17:22Z
---
## Problem

qew create --kind epic --parent ADG fails: a epic cannot sit under a epic. GitHub sub-issues nest to eight levels and foundlings' closeout epic ADG cannot contain its phase epics; needs-edges fake it and show as blocked-by.

## Done when

An epic may have an epic parent; cycles are refused; the mirror sets the sub-issue relation; progress and completable roll up across nested epics.
