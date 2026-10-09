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
Pace creates per forge backend, not globally: GitHub.com defaults to 70 creates/min and 450/hour (GitHub's content-creation limits are about 80/min and 500/hour); GitHub Enterprise Server, Forgejo, Gitea and GitLab default to no pacing because their limits differ or are configurable. Override per [[mirror]] with create_per_minute / create_per_hour (0 = unlimited). One pacer shared by all workers. When the wait would exceed the sync's time budget the sync stops (paced) and a rerun continues. Owner: 'this depends on limits specific by forge backend ... GHE ... forgejo instances etc won't'.
