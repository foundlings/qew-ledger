id: 042cxmtjq
kind: issue
title: Add an installed-wheel smoke walk: build, install in a venv outside the checkout, run the entry point
parent: 042cxmtj6
needs: 042cxmtjn
labels: area:hooks-dist
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
---
## Behaviour
The declared package builds a real wheel (not an empty UNKNOWN one), installs without dependencies into a clean venv, reports the expected name, version and no runtime requirements, and the installed `qew` executable runs `--help` and `--version` and a ledger golden path (init, create, show) from a temp directory without the source tree on sys.path. A symlinked input file to a bulk-import command is refused.

## Scenarios
- Wheel build with no-isolation and pinned tools; metadata `requires` is None. Prevents publishing an empty or dependency-bearing package.
- Installed entry point: help text and a minimal init/create/show walk. Prevents a package missing modules or data that only works from the checkout.
- Symlinked input to the import command is refused (adapt to qew's import walk).

## Reference coverage
1 test (wheel installs executable outside checkout; its plan-apply dry-run part maps to the import walk).

## Qew today
Missing: no distribution test and `pyproject.toml` only declares the build backend (verify project metadata and entry point).
