id: 042cxmtmy
kind: issue
title: Complete `qew list` filters: repeated --label (AND), --owner, --parent, --limit, case folding
parent: 042cxmtmt
needs: 042cxmtmu
labels: area:read-side
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
## Behaviour
`qew list` accepts `--kind`, `--state`, `--label` (repeatable, every label must match), `--owner NAME` (the claimant derived from claim events), `--author NAME` (the actor of the creating event), `--parent ID` and `--limit`. Matching of labels and names is ASCII-case-insensitive (the forge mirrors fold them, so a filter that does not fold hides real work) but never Unicode-folds: a lookalike label such as one using the Kelvin sign must not match the plain label. Rows carry sorted `labels` and the derived `owner`. A filter that matches nothing prints nothing and exits 0.

## Scenarios
- golden: two `--label` flags return only items carrying both. Prevents a one-label match leaking work.
- golden: `--owner alice` returns exactly the items alice currently holds; after `qew release` it returns none. Prevents stale ownership views.
- golden: `--author alice` returns items whose creating event actor is alice. Prevents the person view depending on a mutable label.
- adversary: `--label AREA:CLI` matches `area:cli` but a label spelled with the Kelvin sign does not match `k...`-prefixed labels. Prevents Unicode case folding being used to forge a trusted label.
- golden: rows list `labels` sorted so output is stable. Prevents order churn from file order.

## Reference coverage
Reference read-suite walk: list requires every repeated label; filters by author label and assignee; filters ignore case; rows carry sorted labels and assignees; Kelvin-sign label is not approval (5 tests). `--epic` filter maps to `--parent`.

## Qew today
Reduced. Only `--kind`, `--state`, `--label` (single, exact, case-sensitive); no owner, author, parent, limit, repeat or folding. Covered: `test_list_filters_and_json_output`.
