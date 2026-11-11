id: 044akr10p
kind: issue
title: Flaky: test_edge_walk two-branch edges, ready exits 1 intermittently
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-11-11T07:09:21Z
discovered_from: 044ak8896
---
## Where

tests/test_edge_walk.py test_two_branches_adding_different_edges_keep_both

## Problem

About 1 in 3 solo runs, and once in the full gate, 'ready' after two offline 'block' edits on cloned git ledgers exits 1 (line 61). Find whether ready/replication has a real race or the test needs a settle step.

## Done when

20 consecutive solo runs pass.
