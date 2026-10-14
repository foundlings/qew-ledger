id: 042pzho1g
kind: issue
title: GitHub GraphQL calls never hit the 500,000-node cap silently: adaptive page size, loud named failure, project item cap
parent: 
needs: 
labels: 
owner: 
priority: 1
created: 2026-10-14T16:53:38Z
---
## Problem

GitHub rejects a GraphQL call above 500,000 requested nodes (first/last multiply down the tree), times out after 10 s with a 502/504, and caps a project at 50,000 items. Qew pages boards at a fixed 100, stops at 50 pages (5,000 cards), and reports a node-limit error as an opaque GraphQL rejection.

## Fix

Page size becomes a variable; a node-limit or 502/504 answer halves it (floor 5) and retries, and a floor failure names the query and the limit. Board listings follow the 50,000-item project cap and say so when exceeded. A test estimates every query's worst-case node count and fails above 100,000.

## Done when

A fake that rejects large pages is paged through; a floor failure is loud; a board over the cap is refused naming the cap; the estimator test covers every query constant.
