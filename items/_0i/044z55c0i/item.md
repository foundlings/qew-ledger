id: 044z55c0i
kind: issue
title: The review sync reads every tracked pull request every pass
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-11-22T23:41:02Z
evidence: rlowltom wvtrnuts nzwuukzv
---
## Problem

review_sync.pull reads reviews and inline comments (2 REST calls) of every tracked pull request on every pass; only a record saying merged or closed stops it. foundlings tracks 3264 with 1106 stale open records: about 4500 core calls a pass, the hour's whole budget, retried at every reset.

## Done when

a pass asks the forge one cheap stamp query, reads only changed pull requests, marks finished ones read whatever the record says, and is capped per pass
