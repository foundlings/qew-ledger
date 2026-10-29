id: 042d0fgf4
kind: issue
title: Drive finding: forge labels added by the projection (status:*) are read back as human edits and flood divergences
parent: 
needs: 
labels: drive-finding area:replication
owner: 
priority: 0
created: 2026-10-08T18:17:46Z
evidence: mzyzmozu
---
Seen live on foundlings/qew (3 checkouts, board project 1): sync_plan.labels() emits `status:<column>` but forge_pull's managed-prefix list only knew qew:, kind:, priority:, so every column change looked like a human label edit and produced `forge_divergence` events (21 open after one pass).

Fix: one list of managed prefixes shared by labels() and user_labels(); a mechanical walk proving every label labels() can emit is excluded from user_labels(); existing label divergences of this kind rejected.

Scenario: managed labels never read back as human edits (prevents divergence floods).
