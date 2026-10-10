id: 042d82f60
kind: issue
title: Incremental pull: sync asks the forge only for issues and comments modified since the last pull
parent: 
needs: 
labels: area:replication
owner: 
priority: 0
created: 2026-10-08T20:53:30Z
evidence: oymppymt
---
Owner question: sync should only fetch what changed on the forge since the last time, using 'modified since', not list everything every run.

Today the push side is incremental (pending is derived from event ids) but every sync lists ALL issues of every target (pagination, rate limit). Behaviour: forge.list_issues(since) with since = the last successful pull's start time minus a safety margin (GitHub and Forgejo `since`, GitLab `updated_after`; pull requests are excluded as before); the cursor lives in local state (.qew/state/TARGET/cursor.json, never committed); a full listing runs when there is no cursor, with `qew sync --full`, or when the last full listing is older than a day, and only a full listing may conclude that an issue was deleted on the forge; incremental results merge with the mirrored set by number; a failed pull never advances the cursor; comments and label/title edits bump updated_at on every forge so they arrive; one request in the common no-change case.

Scenarios (fakes honor since): golden: a second sync with no forge changes makes one list request and imports nothing; a human edit made after the cursor arrives, one made before does not repeat; a forge outage mid-pull leaves the cursor unchanged so the next run re-reads the window; a deleted issue is only noticed by the full listing (`--full` or daily); a clock-skewed window (margin) never misses an edit; `qew status` shows the last pull time and whether the next pull is full.
