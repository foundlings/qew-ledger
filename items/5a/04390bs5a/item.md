id: 04390bs5a
kind: issue
title: qew push fails 'more than 50 pages' creating an issue in a repository past the page cap
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-24T03:27:42Z
evidence: mvtkvxvqqwvl lstyyyryxwop
---
## Where

src/qew/forge_github.py find_issue

## Problem

the pre-create lookup lists every issue of the repository; foundlings has more than 50 pages of issues and pull requests, so a new item's issue is never created and later pushes fail too
