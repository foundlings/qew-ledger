id: 042cxmtjf
kind: issue
title: Resolve the hook install root in jj-only, colocated and secondary jj workspaces; refuse outside a repo
parent: 042cxmtj6
needs: 
labels: area:hooks-dist
owner: 
priority: 1
created: 2026-10-08T17:20:13Z
---
## Behaviour
Hook install and remove work from any subdirectory of a plain git checkout, a colocated git+jj checkout and a jj-only checkout with no `.git`, always writing at the nearest ancestor holding `.git` or `.jj`, never creating a private `.git`. Outside any repository they exit 2 with `not inside a Git or jj repository` and create nothing.

## Scenarios
- jj-only root with install run from `apps/web`: files land at the root, not the subdirectory, and no `.git` appears; remove from the subdirectory works. Prevents hooks being impossible in jj-only checkouts, and the forbidden private-git workaround.
- Colocated checkout, install from `crates/`: root wins. Prevents splitting config between nested directories.
- Empty temp dir: exit 2, directory still empty (the outside-repository refusal exists in qew but does not check emptiness).

## Reference coverage
3 tests (the jj sections of the install walk file).

## Qew today
Reduced: only the outside-repo refusal is tested; the two jj layouts are untested although `cmd_hook` supports `.jj`.
