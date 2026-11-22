id: 044yme82r
kind: issue
title: Find what leaves refs/jj/keep/*.lock files behind
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-11-22T17:18:18Z
evidence: twslrlsk xyuzxkot mtzzntrm
---
## Problem

6521 stale refs/jj/keep/*.lock files (about 3 days old) piled up in the foundlings ledger; qew gc could not run until they were removed by hand.

## Done when

the code path that creates keep-ref locks and leaves them is found and fixed, or shown to be jj's own
