id: 042cxmtjt
kind: issue
title: Verify the build checkout equals the recorded source commit before attesting
parent: 042cxmtj6
needs: 042cxmtjr
labels: area:hooks-dist
owner: 
priority: 3
created: 2026-10-08T17:20:13Z
---
## Behaviour
Qew has no forge CI (docs/specs/releases.md), so the reference workflow gate becomes a local release-script step: the working copy commit must equal the source sha passed to the metadata script, the tree must be clean, and the package version must equal the tag.

## Scenarios
- Same commit passes; moved or dirty checkout fails with a message containing 'differs'. Prevents the build and SBOM describing different commits.
- Version/tag mismatch fails before building.
- Tag-name checkout is never used as the source (the local script takes the commit id).

## Reference coverage
2 workflow tests; redesigned as a local script walk because there is no workflow file in qew.

## Qew today
Missing: spec says a single local release script is ledger work not yet done.
