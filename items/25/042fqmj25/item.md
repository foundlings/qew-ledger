id: 042fqmj25
kind: issue
title: Custom Projects v2 fields: a per-mirror map to text and single-select fields
parent: 042fnqu4s
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-10T02:40:54Z
evidence: qputtuvvykql nzrprmyskrqn
---
Split from 042fnquv5 (issue types shipped in 4.17.0). A [[mirror]] option maps ledger facts (kind, priority, area label) to extra Projects v2 fields (single-select and text): push sets them via updateProjectV2ItemFieldValue, the card pull reads them and reports a divergence when a human changes one. Part of the parity list the owner approved ('so it all, aproved'); drafted because it is a separate, larger slice on the board machinery. Off unless the mirror names a map.
