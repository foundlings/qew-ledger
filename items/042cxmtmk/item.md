id: 042cxmtmk
kind: issue
title: Add `qew pr merge --auto`: enable forge auto-merge only where checks are required
parent: 042cxmtm4
needs: 042cxmtmg 042cxmtmj
labels: area:pull-requests
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
## Behaviour
`--auto` lets a PR with pending checks merge once they pass, but only when the base branch requires status checks (branch protection or an active ruleset); otherwise the forge would merge at once and skip CI, so it is refused (exit 3 'would merge immediately'). Rules that cannot be read are an indeterminate failure (exit 4), never assumed. After enabling, the PR is re-read and must show auto-merge enabled, else exit 3. The output names the follow-up (`qew complete`). A forge without auto-merge raises `Unsupported` and exits with a clear line. `--auto` with `--admin` is exit 2 before any call.

## Scenarios
- no required checks: `--auto` with pending checks refused exit 3, zero merge calls. Prevents: auto-merge that skips CI.
- ruleset with required checks accepted though no classic protection rule exists. Prevents: false refusals on ruleset repos.
- ruleset without required checks does not enable auto. Prevents: assuming any ruleset protects.
- rules unreadable (403): exit 4, no merge. Prevents: guessing.
- protected base enables auto and prints follow-up; auto not visible after enabling exit 3.
- forge without auto-merge (Forgejo test double): Unsupported surfaced as one line, nothing written.

## Reference coverage
Reference pr merge walk file: auto refused with no required checks, accepted with ruleset, ruleset without required checks, unreadable rules, auto enables and names landing command, auto not taking effect. 6 test functions, plus part of the contradictory-options test.

## Qew today
Missing: no `--auto`, no `enable_auto_merge` capability on `Forge`.
