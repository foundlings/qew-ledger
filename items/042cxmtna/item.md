id: 042cxmtna
kind: issue
title: Make `qew blocked` explain each unmet need with state and title, and cover blocked edge cases
parent: 042cxmtmt
needs: 042cxmtmu
labels: area:read-side
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
## Behaviour
`blocked` lists open approved or claimed work with at least one unmet need and explains only those needs that are still unmet. JSON carries `blocked_by: [{id, state, title}]` (not bare ids), text carries `<- short ids`. Needs that are completed are not listed; a closed (not completed) or dangling need is listed as unmet, with state `closed` or `missing`. Drafts are never listed, since their gate is approval, not a need.

## Scenarios
- golden: item with one open and one completed need lists only the open need. Prevents false blockage.
- adversary: a closed-as-duplicate need and a dangling need still block and are labelled. Prevents a guessed ready state.
- adversary: a draft with an open need is absent from `blocked` and `ready`. Prevents drafts leaking through the blocked view.
- golden: claimed work with an unmet need is listed with its owner. Prevents hidden stuck work.

## Reference coverage
Reference read-suite blocked golden walk explains only open vetted blockers (1 test).

## Qew today
Reduced. `blocked` prints unmet ids and `blocked_by` as ids; covered in the ledger golden walk; closed/dangling/draft/claimed cases not asserted.
