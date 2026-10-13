id: 042mmrq5j
kind: issue
title: Pre-tool hook costs a full CLI import per Bash call; install cannot leave PreToolUse alone
parent: 
needs: 
labels: 
owner: 
priority: 1
created: 2026-10-13T00:49:45Z
---
## Problem

qew hook pre-tool loads the CLI, config and snapshot code for every shell call, even a plain ls (foundlings measured 1.0-1.8 s wall). A repo that calls the guard from its own gate script cannot stop qew hook install re-adding the PreToolUse entry.

## Done when

A pre-tool event whose command names none of the guarded binaries is answered without importing qew.cli; every refusal still fires; hook install --claude --skip-pre-tool leaves PreToolUse alone.
