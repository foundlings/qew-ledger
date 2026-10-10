id: 042cxmtmb
kind: issue
title: Extend the forge interface: PR body, author, update body, and per-forge support
parent: 042cxmtm4
needs: 
labels: area:pull-requests
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
---
## Behaviour
`RemotePullRequest` gains `body` and `author` (forge login); `Forge` gains `update_pull_request_body(number, body)` (idempotent, returns the re-read PR) and `PullRequestSpec` gains `assignee`. GitHub uses `PATCH /pulls/N`, Forgejo `PATCH /pulls/N`, GitLab `PUT /merge_requests/iid` (description). A null body reads as empty; any other mistyped field is `ForgeRejected`. Anything a forge lacks raises `Unsupported`, never faked. Documented in docs/specs/forges.md.

## Scenarios
- round trip per backend (fake server): open with body, read body, update body, read back differs only by the edit. Prevents: a backend that silently truncates or escapes the body.
- malformed body type is rejected not defaulted. Prevents: fabricated empty bodies hiding a checklist.
- assignee set on open is read back as author/assignee. Prevents: PR ownership drift between forges.

## Reference coverage
Reference gh adapter edit/read operations used by pr check and ownership (no separate test file; exercised by pr check and pr ready walks).

## Qew today
Missing: forge.py and the three backends have no body/author/update support.
