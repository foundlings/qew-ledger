id: 042cxmtgj
kind: issue
title: Create and repair the standard board views, scoped to the target's select expression
parent: 042cxmt4m
needs: 042cxmtgd
labels: area:board-admin
owner: 
priority: 3
created: 2026-10-08T17:20:13Z
evidence: rsrmurwp ynzrmwqk
---
## Behaviour
GitHub boards get views Kanban (board layout, the default view renamed), Table, Ready (`status:Ready`), Blocked (`is:blocked`), Active (`status:"In progress"`), Review (`status:"In review"`), Drafts (`status:Draft`) and Roadmap (roadmap layout). Missing views are created, wrong layout or filter is repaired, views qew does not own are never touched, and a view already scoped by hand is left alone (no update call). When the mirror has a `select` expression whose terms are labels, every qew view filter is prefixed with the equivalent `label:` filter so an unrelated issue that reaches the board stays out of qew's views (the reference's overlay scoping; a mirror selecting everything adds no prefix). Other forges: Unsupported, not faked.

## Scenarios
- `ensure_creates_the_standard_views_once`: second run issues no view mutation; prevents duplicate views.
- `scoped_mirror_prefixes_every_view_filter`: select `label:area:erp` yields filters like `label:area:erp status:Ready`; prevents unrelated issues showing in qew views.
- `hand_scoped_views_survive_ensure`: no view update when filters already match; prevents reverting manual scoping each run.
- `views_not_owned_are_untouched`: a custom 'Mine' view is left alone.

## Reference coverage
Tests: overlay project scopes views to managed issues (eight filters), overlay project keeps views already scoped (no update calls). Spec: projects.md views section.

## Qew today
Missing (no view API in `forge_github`). Priority 3: cosmetic, GitHub only.
