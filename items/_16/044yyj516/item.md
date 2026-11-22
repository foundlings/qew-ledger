id: 044yyj516
kind: epic
title: GitHub pull request reads cost one GraphQL point, not three REST calls
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-11-22T21:26:10Z
evidence_absent: children: all 3 children finished
---
## Problem

read_pull_request makes at least 3 REST calls (the pull, the combined status, the check runs) and every pr verb makes it several times; with 15 agents the shared token's core REST limit hits 0 while GraphQL has 4955 of 5000 left.

## Approach

Read a pull request's whole state, checks included, in one GraphQL query with REST as the fallback; find open pull requests for a head in one query; track core and graphql quota separately; cache the branch protection lookup per process.

## Done when

a pr verb's read path makes no REST read calls on GitHub, the parity walk proves GraphQL and REST give the same RemotePullRequest, the reserve watches the right resource
