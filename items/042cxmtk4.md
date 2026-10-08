id: 042cxmtk4
kind: issue
title: Record the agent lane on a claim (`--lane`, `--workspace`, `--kind`) and show it
parent: 042cxmtjw
needs: 042cxmtjy
labels: area:lifecycle
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
## Behaviour
Several agent lanes often share one actor, so owner alone cannot say which lane holds an item. `qew start ITEM --lane ID [--workspace PATH] [--kind compute|token]` stores `lane`, `workspace` and `kind` in the `claimed` event (kind defaults to compute; absent kind reads as compute). Validation before any write, exit 2: lane is 1-64 of `A-Za-z0-9._-`, starts with a letter or digit, no `--`; workspace is an absolute printable path without `--`; `--workspace` and `--kind` require `--lane`; kind is compute or token. `qew show` (human and `--json`) exposes the current claim as `{by, kind, lane, workspace}` and null when unclaimed. The event schema validates these fields, so a malformed one makes `qew check` fail loudly (the reference skips a malformed comment marker with a warning; events are schema-checked, so loud is correct).

## Scenarios
- golden: start with lane, workspace and kind token; event stores them; `--json` and human `qew show` print the claim (prevents: a lane that cannot be seen by its siblings)
- invalid lane or workspace table (`a--b`, `-x`, relative path, `--` in path, workspace or kind without lane, kind gpu): each exits 2 with zero events (prevents: junk in the claim record)
- claim without kind reads as compute; unclaimed show has `claim: null` (prevents: ambiguous defaults)
- malformed lane field in a hand-edited claimed event: `qew check` fails naming the event (prevents: silently ignored bad data)

## Reference coverage
8 reference test function(s): `test_start_with_lane_records_and_verifies_the_lane_claim`, `test_start_lane_json_names_lane_and_workspace`, `test_start_kind_token_is_recorded_in_the_marker_and_shown`, `test_marker_without_kind_reads_as_compute`, `test_invalid_lane_or_workspace_is_refused_before_any_call`, `test_show_exposes_the_current_lane_claim`, `test_show_unclaimed_issue_has_null_claim_without_extra_read`, `test_malformed_marker_is_ignored_with_a_warning`

## Qew today
Missing. The `claimed` event has only `owner`; `qew show` prints owner only.
