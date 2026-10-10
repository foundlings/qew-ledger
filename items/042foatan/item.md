id: 042foatan
kind: issue
title: Sub-issue calls are paced and can be switched off per mirror
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-10T01:53:48Z
evidence: lzqtunzmqnky kxuqkuzytoux
---
Follow-up to the sub-issue mapping (4.10.0): the first sync after the upgrade sets a parent on every mirrored issue whose parent is mirrored (about 1,800 mutating calls on foundlings). They go through the same create pacing, and a [[mirror]] option sub_issues = false turns the mapping off.
