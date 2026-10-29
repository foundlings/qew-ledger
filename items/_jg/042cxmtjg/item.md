id: 042cxmtjg
kind: issue
title: Verify jj workspace git-store resolution for forge/repo discovery commands
parent: 042cxmtj6
needs: 
labels: area:hooks-dist
owner: 
priority: 2
created: 2026-10-08T17:20:13Z
evidence: yyxqtxwu
---
## Behaviour
Where qew shells out to a tool that needs a git context (repository URL inference for evidence and PR commands), a jj secondary workspace with no `.git` resolves the real git store through the workspace pointer file and the main repository's `store/git_target`, passing it as the git directory. An unresolvable pointer fails loudly (exit 3) naming what could not be resolved. A plain git checkout is left to the tool's own inference.

## Scenarios
- Secondary workspace: the subprocess sees the main checkout's git directory and the inference error does not occur. Prevents commands failing with 'not a git repository' inside a jj workspace.
- Broken pointer: exit 3, message says the git store of this jj workspace cannot be resolved, no subprocess call. Prevents a silent fallback to the wrong repository.
- Plain git: no injected git directory. Prevents overriding a working inference.

## Reference coverage
3 tests (jujutsu workspace walk file).

## Qew today
Code exists (`vcs.workspace_git_dir`, `code_vcs`) with no scenario in the test tree. Missing tests; adapt the fake binary to qew's actual subprocess seam (code_vcs repository URL, forge token lookup).
