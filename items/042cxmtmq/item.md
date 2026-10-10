id: 042cxmtmq
kind: issue
title: Harden untrusted forge and config text at the request boundary
parent: 042cxmtm4
needs: 
labels: area:pull-requests
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
## Behaviour
Mirror `repo` and `api` values are validated at config load: scheme http/https only, no credentials or query/fragment in the URL, owner and repo path segments limited to the forge character set (GitLab allows nested groups); anything else is refused (exit 2) before any request. Forge text (titles, bodies, error detail) is never used as a path, command or URL to follow (Link headers leaving the API root are refused, already enforced for GitHub). PR numbers are positive integers validated before use in a URL path.

## Scenarios
- bad repo/api URL table (`file:///etc/passwd`, `https://user:pw@host/o/r`, `https://host/o/r?x=1`, `https://host/o/ r`): config load refused, zero requests. Prevents: token sent to an attacker host or local file read.
- pr number 0/-3/non-numeric refused before any forge call.
- Link header leaving the API root is refused without following (add for Forgejo and GitLab; GitHub exists).

## Reference coverage
Reference github boundary walk file: repo outside the character set refused before gh (the `@file` upload adversary), plus the unit-level discovery walk. The `@` local-file read is a gh-only hazard, so only its intent (validate the target before any call) is carried here.

## Qew today
Reduced: `forge_http.split_repo` parses the URL without validating it, only GitHub tests the cross-host Link refusal. No config-level URL validation walk.
