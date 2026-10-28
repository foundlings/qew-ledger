id: 042nfdu9w
kind: issue
title: qew sync never removes a blocked-by link after the ledger drops the need
parent: 
needs: 
labels: 
owner: 
priority: 1
created: 2026-10-13T10:34:19Z
evidence: wvwsyqtwwlup knlvzpsmnxsr
---
## Problem

qew set ID --needs (cleared) then qew sync leaves the forge's blocked-by links in place and reports success (foundlings #4301, #4299).

## Done when

sync unlinks the dependencies it created once the ledger no longer needs them (GitHub, Forgejo); links it did not create stay; a rerun sends nothing.
