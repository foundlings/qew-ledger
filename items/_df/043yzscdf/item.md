id: 043yzscdf
kind: issue
title: Expose ready-item impact scores and explicit priority or dependent ranking
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-11-05T13:00:57Z
discovered_from: 043yz92bi
---
## Problem

ready already sorts priority then chain depth then direct dependents, but hides the metrics and provides no alternate ranking or root scope. Agents mistake waiting-item counts for immediate unlocks and manually reconstruct rankings over the whole ledger.

## Fix

Add by-priority and by-dependents ordering, root-scoped candidates, visible rank and priority plus direct/transitive open dependents, immediate unlocks and chain depth in text and JSON. Keep the default priority ordering and explain its precedence.

## Done when

Command walks prove priority versus impact ordering, diamond deduplication, AND-gate immediate unlocks, finished/gated exclusions and scoped candidates; docs and help agree; the combined release gate passes.
