id: 042cxmtjr
kind: issue
title: Pin release metadata: SPDX 2.3 SBOM, SHA256SUMS, refusals
parent: 042cxmtj6
needs: 
labels: area:hooks-dist
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
evidence: xxklssuy
---
## Behaviour
`scripts/release_metadata.py` writes a deterministic SPDX 2.3 document (name, creation time normalized to UTC from an offset timestamp, package name/version/license/purl, DESCRIBES relationship) and SHA256SUMS listing every dist artifact plus the SBOM in sorted order. Symlinks and non-regular files in dist are refused; checksums inside dist are refused (they would upload as a duplicate); version and source sha are validated.

## Scenarios
- Golden: wheel and sdist produce SBOM fields and the exact checksum lines (covered by the qew metadata walk).
- Symlinked artifact refused (`regular files`) (covered).
- Checksums inside dist refused with exit 2 and file not created (covered).
- NEW: bad version, short source sha, naive timestamp, empty dist each refused; two runs produce identical bytes. Prevents non-reproducible or malformed attestations.

## Reference coverage
3 tests.

## Qew today
Covered 3/3; only the validation rows are missing.
