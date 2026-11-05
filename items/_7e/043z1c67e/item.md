id: 043z1c67e
kind: issue
title: Use the worker lock rather than startup grace for queued-work handoff
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-11-05T13:32:56Z
discovered_from: 043yz92bi
---
## Problem

The release gate again synced only five of six burst writes. A worker exiting with queued ids calls queue, which can mistake a fresh or stale provisional sync.starting marker for an active worker and leave the tail queued. Publishing the marker before spawn does not cover this handoff case.

## Fix

On worker handoff, consult the authoritative sync.lock instead of provisional startup grace. Keep normal spawn coalescing and retry backoff. Add deterministic stale-marker and active-worker refusal walks.

## Done when

An exiting worker cannot leave queued work blocked solely by startup grace; a real active worker still prevents a competing spawn; burst and full gate walks pass.
