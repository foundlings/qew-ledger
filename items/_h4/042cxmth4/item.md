id: 042cxmth4
kind: issue
title: Seven-status model: derive the board status for every item
parent: 042cxmth3
needs: 
labels: area:project-parity area:board
owner: 
priority: 0
created: 2026-10-08T17:20:13Z
evidence: ytnnyxvt
---
Decision: the board has seven Status values (this supersedes the five-column text in the brief). Derivation, first match wins: completed/closed -> Done; draft -> Draft; epic -> In progress only while a direct child is claimed, else Backlog; label `needs:approval` -> Needs approval (outranks claim, review, blockers); not triaged (missing kind or priority) -> Draft; open linked PR mirror -> In review; claimed -> In progress; approved with every need completed -> Ready; else Backlog.
Status options: Draft (GRAY) 'Not workable yet: drafts, and work missing approval, a type or a priority'; Backlog (GREEN) 'Approved but blocked, deferred, or a planning container'; Ready (BLUE) 'Qew reports this work as actionable now'; Needs approval (PINK) 'Waiting for a human to authorize the work before it may start'; In progress (YELLOW) 'Claimed and actively being implemented'; In review (PURPLE) 'Implementation has an open linked pull request'; Done (ORANGE) 'Closed and completed'.
Scenarios (named walks, each stating the failure it prevents):
- golden: one ledger per status shows the expected column
- adversary: needs:approval on a claimed item still shows Needs approval
- golden: an epic is Backlog until a child is claimed, then In progress
- prevents the offline board, the sync projection and `qew ready` disagreeing about the same item
