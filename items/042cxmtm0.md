id: 042cxmtm0
kind: issue
title: Legacy Status option migration
parent: 042cxmth3
needs: 042cxmtky
labels: area:project-parity board
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
---
An old option name (the reference's `To triage`) is renamed in place to the new one keeping its id and cards, or dropped when the new option already exists; unknown foreign options are preserved and reported.
Scenarios (named walks, each stating the failure it prevents):
- golden: legacy option renamed, cards stay
- golden: legacy and new both present: legacy dropped after its cards move
- adversary: a foreign option with the same name but different color is left alone and reported
