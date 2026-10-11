id: 042ie9g1p
kind: issue
title: The evidence push hook checks commits already published on other branches and reads prose after Refs: as item ids
parent: 
needs: 
labels: 
owner: 
priority: 1
created: 2026-10-11T10:33:01Z
---
Rudolph (foundlings integrator) blocked pushing PR #4391: the jj push guard checks every commit in the pushed revset including elves' commits already on their PR branches (it demands qew evidence for items claimed by other actors), and 'Refs: 042h3tmc9. Generated only through ...' reports Generated/only/through as unknown ledger items. Fix: check only commits not reachable from any remote ref; parse only the leading id tokens of a Refs trailer, stopping at the first non-id token or sentence end.
