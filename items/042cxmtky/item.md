id: 042cxmtky
kind: issue
title: project ensure builds the full board: Status options, Priority field, views
parent: 042cxmth3
needs: 042cxmth4
labels: area:project-parity area:board
owner: 
priority: 0
created: 2026-10-08T17:20:13Z
evidence: rsrmurwp
---
Status options: Draft (GRAY) 'Not workable yet: drafts, and work missing approval, a type or a priority'; Backlog (GREEN) 'Approved but blocked, deferred, or a planning container'; Ready (BLUE) 'Qew reports this work as actionable now'; Needs approval (PINK) 'Waiting for a human to authorize the work before it may start'; In progress (YELLOW) 'Claimed and actively being implemented'; In review (PURPLE) 'Implementation has an open linked pull request'; Done (ORANGE) 'Closed and completed'.
Priority field options P0 RED 'Critical priority', P1 ORANGE 'High priority', P2 YELLOW 'Normal priority', P3 GREEN 'Low priority', P4 GRAY 'Backlog priority'.
Views in order: Kanban (BOARD_LAYOUT, the default view renamed), Table (TABLE_LAYOUT), Ready (filter status:Ready), Blocked (is:blocked), Active (status:"In progress"), Review (status:"In review"), Drafts (status:Draft), Roadmap (ROADMAP_LAYOUT).
The Status options are created with their colors and descriptions in this order; the Priority field carries P0-P4 with colors and descriptions; every view is created or its layout/filter corrected; extra human views are left alone. Idempotent; recorded in boards/ in the ledger.
Scenarios (named walks, each stating the failure it prevents):
- golden: GitHub fake receives the seven options, five priorities and eight views exactly once; prevents duplicate projects and fields on re-run
- adversary: a view whose filter was edited on the forge is corrected and reported
- refusal: forge without boards reports unsupported, exit 0
- adversary: a project renamed by a human is found by recorded id, not title
