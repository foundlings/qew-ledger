id: 044qiiq1f
kind: issue
title: pr merge --check (ledger-only and forge) re-scans every item's mirrors per pull request: 26-PR union takes 373 s
parent: 
needs: 
labels: 
owner: 
priority: 0
created: 2026-11-18T17:03:00Z
discovered_from: 044qdr89f
evidence: kpqlnmmu
---
## Problem

pr_record.find walks every item and loads its mirrors for each PR number, and the legacy conflict scan repeats it per covered item: cost is items x PRs. Foundlings 26-PR union: 373 s ledger-only, 218 s forge check; the gate kills qew at 180 s.

## Done when

one PR index built once per snapshot serves every number; 26 PRs under 15 s and one PR under 5 s on the Foundlings ledger; a regression test fails when mirror loads grow with the PR count; released as 6.57.1
