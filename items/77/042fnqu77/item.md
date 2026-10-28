id: 042fnqu77
kind: issue
title: Sub-issues: the ledger parent shows as GitHub's native sub-issue relation
parent: 042fnqu4s
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-10T01:42:09Z
evidence: polpypmrnpvm olzswqxrtpvl
---
Push: an item whose parent is mirrored becomes a sub-issue of the parent's issue (REST sub_issues, which takes the child's issue id, not number); a parent change moves it; a removed parent removes the relation. Pull: a sub-issue relation made on GitHub that the ledger does not hold is a divergence (field parent), never applied silently. Idempotent: the mirror record remembers the relation it last wrote. Epics/issues/tasks follow the ledger kinds; tasks stay ledger-only as today.
