id: 042o51a63
kind: issue
title: claim withdrawal released an epic's reservation twice (gate failure shipped in 6.21.0)
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-13T18:57:25Z
evidence: mrtkuomktuln qwlusovsvvst
---
6.21.0 shipped with test_epic_claim_walk failing: _start_epic released its reservations and the session withdrew them again. Released claims leave the posted list.
