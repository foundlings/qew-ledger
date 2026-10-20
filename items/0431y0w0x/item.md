id: 0431y0w0x
kind: issue
title: qew list --recent [N] and --since: the newest items first, by creation time
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-20T15:18:26Z
evidence: tpxkumssyszt lzpxlvlovxuv
---
qew list has no recency view: it returns every item in priority order, so checking whether an item was just created needs a keyword qew search. Add --recent [N] (newest first by creation time, default 100) and --since TIME|DURATION (created at or after an instant, a date, or a relative age such as 2h or 3d), combining with the existing list filters and --json.
