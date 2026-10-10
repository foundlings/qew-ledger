id: 042cxmtha
kind: issue
title: Board filter expressions using the select syntax
parent: 042cxmth2
needs: 042cxmth6
labels: area:board
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
evidence: lutuzxmp
---
`--filter` takes the same `label:X kind:X state:X priority:N` terms (spaces and, commas or) plus `owner:X`, `epic:ID`, `parent:ID`.
Scenarios:
- golden: filter narrows cards and counts
- refusal: malformed term exits 2; prevents an empty board that looks like no work
