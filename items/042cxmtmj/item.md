id: 042cxmtmj
kind: issue
title: Add forge capability: read whether the base branch requires status checks
parent: 042cxmtm4
needs: 
labels: area:pull-requests
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
## Behaviour
`Forge.requires_status_checks(branch) -> bool` (typed; `Unsupported` where unknown) answers from branch protection or active rulesets (GitHub REST `rules/branches/{b}` and protection), GitLab protected-branch + project setting `only_allow_merge_if_pipeline_succeeds`, Forgejo branch protection `enable_status_check`. Read failures are typed forge errors, never False. Documented in forges.md.

## Scenarios
- per backend fake: protected -> True, none -> False, 403 -> ForgeAuth. Prevents: treating an unreadable rule set as 'no checks required'.

## Reference coverage
Supports pr-merge-auto and pr-merge-admin; reference rules-read tests (4) map to the command issue.

## Qew today
Missing.
