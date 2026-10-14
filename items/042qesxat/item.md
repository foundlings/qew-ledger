id: 042qesxat
kind: task
title: qew land is refused for a non-opener: nothing-open PRs exit 3 and --integrator cannot land another actor's items
parent: 
needs: 
labels: 
owner: 
priority: 1
created: 2026-10-14T22:05:52Z
---
land runs pr_record.require_owner before its own per-item holder check, so a caller who did not open the PR is refused (exit 3, 'no open item') when every covered item is complete, and --integrator is refused when it holds none of the claims. Land checks each item's holder itself; skip the PR-level rule. All complete: print 'nothing to land: all covered items complete', exit 0. Reported by foundlings on 13 PRs (#4459).
