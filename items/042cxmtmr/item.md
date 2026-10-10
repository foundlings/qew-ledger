id: 042cxmtmr
kind: issue
title: Prove complete pagination for the forge reads the pr commands rely on
parent: 042cxmtm4
needs: 
labels: area:pull-requests
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
## Behaviour
Reads of pull requests, checks, labels and issue lists complete every page up to `MAX_PAGES` and raise `ForgeRejected` beyond it or when a Link leaves the API root; they never return a truncated list as if complete. Check-run folding (GitHub combined status plus all check runs) counts every page: one failing check on page two makes the PR `failing`. A GraphQL error body is a typed failure with the server message, not a default value.

## Scenarios
- checks span two pages with a failure on page 2: PR checks read `failing`. Prevents: merging a red PR because page 1 was green.
- endless pagination bounded for PR and check reads (exists for issue lists on GitHub and Forgejo, add for check runs and GitLab).
- GraphQL error with message becomes ForgeRejected carrying the message (covered for GitHub `test_graphql_errors_are_typed`). Prevents: reading an error body as data.

## Reference coverage
Reference github boundary walk file: every paginated query puts its own pageInfo first (gh-specific, dropped), top-level issue pages merged, nested blocker pages completed, GraphQL errors fail closed, last page claiming more data refused. 5 test functions map to the pagination/GraphQL scenarios here.

## Qew today
Covered in part: GitHub walk has endless-pagination bound, cross-host Link refusal, GraphQL typing; Forgejo has the pagination bound; GitLab has `find` paging. Missing: check-run pagination scenario and GitLab/Forgejo link-host walks.
