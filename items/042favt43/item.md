id: 042favt43
kind: issue
title: Pace adapts after a secondary-limit block: halve the create rate, remember the observed budget, resume at the learned pace
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-09T21:40:03Z
---
Santa 2026-10-09: GitHub still blocked content creation every ~250 creates per round even at 70/min, so this account's real budget looks like ~250 per 20-30 min, not 450/hour. The fixed GitHub.com default is a guess. Idea: when a secondary-limit 403 arrives, record how many creates preceded it (per target, local state), and on the next run pace under that observed budget (for example 80 percent of it per window), relaxing slowly while no block occurs. Keep the per-mirror create_per_minute / create_per_hour overrides as the owner's explicit control. Draft: needs the owner's approval before building.
