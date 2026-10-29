id: 042f15ycm
kind: issue
title: Type hints and a type checker for qew on Python 3.15, in a new pull request
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-09T18:21:48Z
evidence: zmoqpwotvzyw ykmzoszzvznq
---
Owner 2026-10-09: upgrade qew with complete type hints and a type checker; brew-upgrade Python to 3.15 and use 3.15's typing features (https://docs.python.org/3/library/typing.html). Its own pull request, after the Santa items (close reasons, sync speed, parallel writes).

Requirements: the checker must reject untyped code. Configure it strict: every function and method fully annotated (parameters and returns), missing annotations and implicit Any are errors, not warnings (e.g. mypy --strict / disallow_untyped_defs, or pyright strict / ty equivalents; pick one that supports 3.15 and justify). Warnings the checker emits are promoted to errors. The check runs in scripts/gate.py and has its own test proving it fails on an unannotated function and passes on an annotated one. Dev-only tool, never a runtime dependency (runtime stays stdlib-only). Raise the minimum Python to 3.15 and update CLAUDE.md, README and setup. CLAUDE.md already states the rule that typing is part of the tests.
