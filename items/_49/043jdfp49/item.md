id: 043jdfp49
kind: issue
title: Schema 8 regression: every per-item alias lookup re-stats all ~1200 shards, so check/sync/pr commands take tens of minutes on 25k items
parent: 
needs: 
labels: 
owner: 
priority: 0
created: 2026-10-29T07:01:14Z
evidence: wxwztovpomsy vpsrlwzlopks
---
ledger_aliases.scan calls ledger_layout.stamp (root scandir + one stat per shard) on every aliases() call; _homes()/load_mirrors/baseline lookups call aliases() once per item, so a whole-ledger command does items x shards stats (check and sync --all: 42 stamps for 40 items). Flat layout paid one stat. Fix: do not re-stamp on every call.
