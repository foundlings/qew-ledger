id: 042cxmtjp
kind: issue
title: Pin the user setup script walks: link, rerun, PATH warning, foreign file, unsupported system
parent: 042cxmtj6
needs: 
labels: area:hooks-dist
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
evidence: xxklssuy
---
## Behaviour
`scripts/setup_user.py` creates a virtualenv under XDG data home, installs the checkout, and symlinks `qew` into `~/.local/bin`; rerun is idempotent; it warns when the directory is not on PATH; refuses to replace any file it does not own (exit 2); unsupported OS exits 2; failed environment/install commands exit 3.

## Scenarios
- Golden: fresh HOME, link runs `qew --help` successfully, rerun still a symlink, no PATH warning (covered).
- PATH warning exit 0 (covered).
- Foreign file refused, content intact (covered).
- NEW: a symlink pointing elsewhere (not its venv) is refused; an own stale symlink is replaced. Prevents clobbering a user-managed link.
- NEW: install command failure exits 3 and leaves no half link.

## Reference coverage
3 tests (link+idempotent, PATH warning, foreign file).

## Qew today
Covered for the 3 reference scenarios; two additions missing.
