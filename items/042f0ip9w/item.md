id: 042f0ip9w
kind: issue
title: A full first sync of a big repo is still about one issue per minute: find the per-create cost with QEW_TRACE and remove it
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-09T18:08:49Z
---
Owner/Santa 2026-10-09: after 8859784d a real foundlings sync (2,400+ issues, 34 pre-existing, many PRs, project 2) still creates about 1 issue per minute. Measure per-create HTTP calls with QEW_TRACE=1 against a fake repo of 2,400 issues plus a project; remove every per-create cost that grows with the repo or board.
