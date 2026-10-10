id: 042cxmtma
kind: issue
title: Derive and verify the pushed head branch (git and jj), with explicit `--head` and issue/branch checks
parent: 042cxmtm4
needs: 
labels: area:pull-requests
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
---
## Behaviour
Without `--head`, the head is derived from the checkout: git needs a named branch (not detached), a clean tree, a matching upstream and zero ahead/behind; jj (a `.jj` found before `.git`) uses the single bookmark at `@` (or `@-` when `@` is empty) that must equal `NAME@origin`, and git is never run there. `--head BRANCH` skips derivation (the caller has pushed; names starting with `-` or containing newline/quote/backslash are refused). A failed probe names its argv and exit status. A branch that names a different ledger item than the one opened is refused with both ids; a branch that names no item is accepted when the item is explicit.

## Scenarios
- unpushed branch: git branch ahead of upstream -> exit 3 'must exactly match its upstream', no forge call. Prevents: a PR for commits the forge cannot see.
- explicit head skips probes: `--head feat/x` with a broken git succeeds. Prevents: derivation failures blocking a caller who knows the branch.
- branch names no item with explicit item accepted; branch naming another item refused with both ids and no forge call. Prevents: a PR attached to the wrong item.
- detached HEAD and failing probe: exit 3, message names the `--head` escape hatch and the failing argv with its exit status. Prevents: opaque errors.
- jj workspace uses its bookmark and never runs git (a git shim that fails when `.jj` exists). Prevents: the shared colocated git HEAD being touched.
- jj bookmark ahead of origin refused; jj failed probe names `jj bookmark list` and exit status. Prevents: PR from a stale remote bookmark.

## Reference coverage
Reference pull-request lifecycle walk file: not-pushed seam, explicit head, explicit issue + unnumbered branch, neither issue nor numbered branch, unrelated head, failed git probe, three jj walks. 9 test functions (several fold into this and pr-open-golden).

## Qew today
Reduced: `vcs.synced_branch` implements git and jj derivation, the `--head` validation and the probe error text, but no test exercises it (tests/test_pr_walk.py passes `--head` directly). Missing: the branch-names-another-item check (qew ids are ULID-like, so the rule is 'branch contains a different known item alias'), and all fake-git/fake-jj walks.
