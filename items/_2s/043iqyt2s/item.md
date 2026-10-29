id: 043iqyt2s
kind: issue
title: scripts/gate.py --changed: run only the test modules and type checks a change can affect, in parallel, slowest first
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-28T23:22:13Z
---
## Goal

gate.py --changed picks modules from a recorded per-module map of the src files they ran, runs them on every core with the scoped type check beside them, and the full gate stays the release gate and refreshes the map
