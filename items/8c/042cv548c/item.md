id: 042cv548c
kind: issue
title: Verify the GitHub Projects v2 GraphQL shapes against real GitHub
parent: 042cv548a
needs: 
labels: 
owner: 
priority: 1
created: 2026-10-08T16:29:39Z
evidence: f552243456de6cdc2fad216444c5fa6c3a4cebc2
---
forge_github board calls (createProjectV2, createProjectV2Field, updateProjectV2Field input shapes) were written against a local fake from memory. Run `qew project ensure` against a scratch repo and fix any drift; capture the real shapes in tests/fake_github.py.
