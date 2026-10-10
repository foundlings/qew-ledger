id: 042cv54dw
kind: issue
title: Local release script for qew 3.0.0 (no GitHub Actions)
parent: 042cv548a
needs: 
labels: 
owner: 
priority: 3
created: 2026-10-08T16:29:39Z
---
Add one local script that runs the release steps in docs/specs/releases.md: tests, build with the pinned tools, scripts/release_metadata.py, scripts/upload_release.py. No GitHub workflows, by owner ruling. Tag only after the owner approves.
