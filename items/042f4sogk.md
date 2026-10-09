id: 042f4sogk
kind: issue
title: Bulk sync paces forge creates under GitHub's content-creation limits (about 80 per minute, 500 per hour)
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-09T19:35:43Z
---
Santa measured 25-35 creates/min with forge_concurrency 4 until GitHub's secondary limit blocked content creation at 498 creates (~25 min). Pace creates proactively under a configurable rate (default under 80/min and 500/hour) instead of hitting the wall, shared across workers, and report the pace. Needs a walk with a fake that blocks after N creates per window.
