id: 042cxmtk6
kind: issue
title: Enforce a per-actor active-claim cap from config (`max_active_claims`)
parent: 042cxmtjw
needs: 042cxmtjy
labels: area:lifecycle
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
evidence: opppyqtx
---
## Behaviour
Agent fleets run many lanes under one actor; an idle loop must not claim more work than can run. `.qew/config.toml` accepts a positive integer cap. `qew start` counts the caller's currently claimed items from the fold after the availability checks and refuses at the cap with exit 6 before any event (count is per actor because the config is shared by everyone in the repo). Without a cap no count is read. A malformed cap (0, negative, string, boolean, float) is invalid configuration, exit 2, naming the key, before any ledger access. Claims left by dead lanes count until released. In a ledger the count is exact for one checkout; merged branches can briefly exceed it, which the spec states.

## Scenarios
- at the cap: exit 6 naming `max_active_claims` and the number, no event (prevents: runaway claiming)
- below the cap: claims as before
- no cap configured: no extra work, claims as before (prevents: cost and behaviour change for everyone else)
- malformed cap table (0, -1, "3", true, 2.5): each exit 2 naming the key, zero events (prevents: a typo silently disabling or breaking the cap)
- take-over counts toward the cap of the taker (prevents: bypassing the cap through take-over)

## Reference coverage
4 reference test function(s): `test_start_at_the_cap_is_refused_before_any_write`, `test_start_below_the_cap_claims_as_before`, `test_without_a_cap_no_count_is_read`, `test_malformed_cap_is_invalid_configuration`

## Qew today
Missing. No config key, no counting, exit 6 unused. The priority-triage case test_priority_triage_is_not_written_at_the_cap is dropped (qew has no start-time triage write).
