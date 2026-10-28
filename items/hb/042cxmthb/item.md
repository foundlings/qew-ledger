id: 042cxmthb
kind: issue
title: Board compact agent format and --json
parent: 042cxmth2
needs: 042cxmth6
labels: area:board
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
evidence: xkvmwvkx
---
Token-efficient fixed-format lines per card plus a stable `--json` schema.
Scenarios:
- golden: json round-trips ids/columns; prevents format drift
- golden: compact output under a byte budget for 200 cards
