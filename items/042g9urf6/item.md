id: 042g9urf6
kind: issue
title: PR review import: a tracked pull request that is gone (404) fails every pull
parent: 042fnqu4s
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-10T09:13:36Z
---
Found by qew sync on qew's own ledger: mirror github-github.com-foundlings-qew-pr-1 names a pull request that does not exist on GitHub; the review read answers 404 and the whole pull reports failed on every sync. A 404 on the review reads means the PR is gone: skip it and remember it as read.
