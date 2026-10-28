id: 042jeppcm
kind: issue
title: Add Progress items to an existing pull request through qew
parent: 
needs: 
labels: area:pull-requests
owner: 
priority: 1
created: 2026-10-11T22:36:29Z
evidence: ylymkzxmkyll wlkzsvpxurnr
---
Current need: Foundlings PR #4402 gained discovered tasks 042jcak6d and 042jcot9f after opening. The required per-item Progress markers cannot be added through qew 6.12.0: pr help offers open/check/ready/label/close/sync/merge; check offers tick/list/drop only. The command-level negative control qew pr body --help exits 2 with invalid choice, while qew pr check --help succeeds. No forge bypass was used.

Provide an owned-open-PR operation that adds marked Progress entries while preserving existing body bytes and checkbox states. Validate item references and duplicate markers; refuse closed or merged PRs, foreign ownership, closing references, and concurrent body changes. Walk the add/read/tick path and each refusal over the existing forge fake. Keep CLI help, command docs and README in agreement.
