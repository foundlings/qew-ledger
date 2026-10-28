id: 042cxmtgs
kind: issue
title: Harden marker-based adoption of forge issues against quoted or forged markers
parent: 042cxmt4m
needs: 
labels: area:board-admin
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
evidence: ntxvlqvt
---
## Behaviour
`find_issue(marker)` is the crash-recovery path: after a crash it adopts the forge issue carrying `<!-- qew:ID -->` instead of creating a duplicate. Today every backend uses a substring test, so an untrusted issue body that merely QUOTES the marker (or an unrelated issue on a shared repo) is adopted and then overwritten by the next sync. Rules, shared by all three backends via one helper: the marker must be the first line of the body or stand alone on its own line; the id inside must match the item's id exactly and be well formed (malformed or case-altered ids never match); an issue that is a pull request is skipped (exists); at most one match: two issues carrying the marker is a typed error naming both numbers, not a pick-the-first; a match whose opener differs from the token's user is reported (warning, not refused) since a collaborator may legitimately have created it. A dry run (`qew sync --dry-run`) lists would-adopt without writing.

## Scenarios
- `quoted_marker_inside_a_sentence_is_not_adopted`: body 'see <!-- qew:ID --> for details' is ignored and a fresh issue is created; prevents hijacking a foreign issue.
- `malformed_or_recased_markers_do_not_match`: table of three bad markers; prevents loose matching.
- `two_issues_carrying_the_marker_fail_loudly`: no silent first-pick; prevents adopting the wrong duplicate.
- `marker_alone_on_a_line_after_a_crash_is_adopted_once`: golden crash walk (existing) keeps passing; prevents duplicates.
- `adoption_is_listed_in_the_dry_run`: dry run names the issue it would adopt and writes nothing.

## Reference coverage
Tests (adopt walk, 7): adopts only approved issues with a provenance marker, without author every opener in scope, marker must stand alone on a line, malformed marker is not a marker, dry run writes nothing, invalid author refused before any call, labels that did not persist are indeterminate. The label-adoption command itself is dropped (no managed label); the marker rules and dry-run map here.

## Qew today
Reduced. Crash adoption works (tests/test_sync_walk.py `test_a_crash_after_create_adopts_the_existing_issue_instead_of_duplicating`), but `forge_github.find_issue` uses `marker in body`; Forgejo/GitLab likewise. No strict-marker test.
