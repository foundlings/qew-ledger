id: 042g5fi2w
kind: issue
title: qew start refuses a ledger-only task: claims must arbitrate through the nearest mirrored ancestor
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-10T07:43:38Z
evidence: txpksukkrmxz msxxpwtqkpyw txpksukkkmvl msxxpwtqwqrr
---
Reported by Santa (foundlings-ledger 042g5cyak, elf5), reproduced on 5.0.0. With a forge as claim authority, claim_authority._primary_forge needs an issue mirror record for the item itself, so a task (mirrors select kind:epic,issue) can never be started: 'the primary forge has no issue for it yet'. Fix: use the item's own issue, else the nearest mirrored ancestor's; the claim and release marker comments already name the item id, so one issue can carry markers for its ledger-only descendants. No mirrored ancestor: the refusal stays. Walk: start through the epic's issue, rival refused, release frees it.
