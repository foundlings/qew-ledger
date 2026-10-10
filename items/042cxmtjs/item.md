id: 042cxmtjs
kind: issue
title: Pin the upload script's host and fixed arguments
parent: 042cxmtj6
needs: 
labels: area:hooks-dist
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
## Behaviour
`scripts/upload_release.py` calls the forge CLI as `release upload TAG FILES... --repo REPO --clobber` with the host taken from the server URL environment variable, port retained; a URL that is not an HTTPS origin (credentials, path, query, fragment) is refused.

## Scenarios
- Enterprise host reaches the CLI as its host variable plus fixed argv (covered).
- Non-default port retained (covered).
- NEW: refused URLs (http scheme, userinfo, path, query) exit nonzero and never invoke the CLI. Prevents sending a token to an attacker-chosen host.
- Forge-specific upload for non-GitHub mirrors is a separate decision.

## Reference coverage
2 tests.

## Qew today
Covered 2/2; refusals missing.
