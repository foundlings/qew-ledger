id: 043hkyffg
kind: issue
title: qew complete and land: a change on the forge's main (main@origin) is landed even when local main is behind or diverged from it
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-28T09:45:20Z
evidence: 5b7cdfc7 c1a2fac2
---
## Goal

a jj checkout whose local main bookmark does not hold a merged change but main@origin does lands and completes it instead of refusing 'not an ancestor of main'
