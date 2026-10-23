id: 0437v33dk
kind: issue
title: A pull request split by qew pr check --drop still covers the dropped root: merge refuses half-done work and the title stays
parent: 
needs: 
labels: 
owner: 
priority: 1
created: 2026-10-23T13:45:58Z
---
## Problem

dropping a root's Progress box leaves it in the pull request record's covered items, so qew pr merge --check refuses its open children and qew pr sync retitles from the dropped root; foundlings PR 4917 is blocked on this.

## Done when

drop removes the item from the covered set (the last one is refused), sync --items does not re-add it, and pr sync titles from the first covered item
