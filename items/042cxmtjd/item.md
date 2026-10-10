id: 042cxmtjd
kind: issue
title: Close the safe-write foundation test gaps (modes, root symlink, tmp cleanup, fsync order)
parent: 042cxmtj6
needs: 
labels: area:hooks-dist
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
## Behaviour
The hook config foundation: atomic same-directory temp file, flush plus fsync, atomic replace, directory fsync; temp file removed on failure; symlinked root, directory component or target file refused (`symlink`); no-op does not rewrite; new directories 0700 and files 0600, existing file mode preserved; removal never creates directories; unmarked managed file never overwritten or deleted.

## Scenarios
- Structural JSON install/remove idempotent, unknown keys kept (covered by the qew hook config walk).
- Managed file install/remove idempotent and refuses an unowned file, which stays byte-identical (covered).
- Symlinked directory and symlinked target both refused and the outside file stays untouched (covered).
- Failed atomic replace leaves the original bytes and no `.NAME.*.tmp` leftover (covered).
- NEW: an existing 0644 or 0640 file keeps its mode after install and after a no-op; new files and directories are 0700/0600. Prevents loosening or tightening a user's config permissions.
- NEW: symlinked repository root and a symlink swapped in after the first lookup are refused (O_NOFOLLOW chain). Prevents writing through a planted link outside the checkout.
- NEW: managed-file remove of an unowned file is a no-op, not a delete.

## Reference coverage
4 tests (json structural, managed file, symlink, failed replace): all four have a qew twin of the same name.

## Qew today
Covered for four scenarios. Missing: preserved-mode, symlink root, unowned remove.
