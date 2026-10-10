id: 042gm5d6t
kind: issue
title: A ledger commit must leave nothing it wrote uncommitted (migrate-layout left qew-ledger.toml dirty on foundlings)
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-10T13:04:23Z
---
Santa: foundlings-ledger commit 4bfc8bec6 (5.0.0 migrate-layout, 20880 files) did not contain the qew-ledger.toml schema_version change; HEAD still says schema_version 2 while the working copy holds 3. Not reproduced here at 1500 files on git or on qew's own jj ledger, so make the commit self-verifying: after repo.commit every journaled path must be clean; leftovers are committed once more, and if any remain the command fails (rolled back where it can be) naming them.
