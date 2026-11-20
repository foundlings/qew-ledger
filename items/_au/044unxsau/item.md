id: 044unxsau
kind: issue
title: An item whose recorded evidence names a change id that does not exist cannot be completed or repaired, although a good id on main is also recorded
parent: 
needs: 
labels: 
owner: 
priority: 0
created: 2026-11-20T18:11:12Z
---
## Problem

Santa/integrator 2026-11-20: after union S merged, 044tp182k (#7782) stays stuck: its evidence includes change id uvuywukowkuuwzmqprpyrntnqsyxysyu which is not in the repo, so qew complete refuses; qew evidence --repair refuses because the item is not completed, so the bad id cannot be dropped. The good id pnmppwrxxowkppuxsqlzwvuorqqltkrn (the head of #7782) is on main.

## Done when

An item with one good landed evidence id and one id that does not resolve completes (or can be repaired in place) without hand-editing the ledger; the walk covers complete, land and evidence --repair on a claimed item.
