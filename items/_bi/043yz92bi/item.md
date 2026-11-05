id: 043yz92bi
kind: issue
title: Traverse and draw scoped item graphs from any node in graph and progress
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-11-05T12:50:17Z
evidence: trtzntqn orywpzqs pllywruq
---
## Problem

graph draws the entire ledger and progress only follows children, so agents rebuild needs graphs and cannot draw the dependency view rooted at ADU.

## Fix

Add explicit edge traversal from selected roots to graph and progress, reverse relationships, depth and open/unmet filters, terminal graph views and structured JSON. Preserve shared links, count shared leaves once and keep existing default output compatible.

## Done when

Command walks cover rooted diamonds, reverse edges, isolated and missing nodes, cycles, depth and filtering, safe labels and unchanged defaults; docs and help agree; gate passes and capabilities are installed.
