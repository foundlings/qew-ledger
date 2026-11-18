id: 044qj4o63
kind: issue
title: Full ledger snapshot takes 13-20 s on the 60k-event Foundlings ledger: profile and cut it
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-11-18T17:15:13Z
discovered_from: 044qiiq1f
---
## Problem

Any command that reads the whole ledger pays one full snapshot (QEW_TRACE shows 'ledger snapshot (full)' 13.8-19.8 s on a loaded machine, mostly waiting on stat of ~25k items and event dirs). It is now the floor of pr merge --check --ledger-only.

## Done when

profile (measure_reads.py) names where the time goes; a one-PR ledger-only check on the Foundlings ledger takes under 5 s, or the remaining floor is explained
