id: 044ro5f8m
kind: issue
title: qew gc --now needs the write lock ahead of queued writers, and the audit note names open pull requests whose items are already finished
parent: 
needs: 
labels: 
owner: 
priority: 1
created: 2026-11-19T06:31:55Z
evidence: zkvllsvzonvs
---
## Problem

Santa 2026-11-19: qew gc --now could not get the write lock (waited 120s behind creates that each hold it 4-5 minutes); and qew check warns open pull requests all close X for 11 pull requests already merged on the forge whose items are completed (mirrors stay open when a pull request is merged outside qew).

## Done when

An urgent taker (qew gc --now) skips the earlier-waiter courtesy and waits up to 30 minutes; the automatic collector waits its turn politely up to 30 minutes. qew check does not note open pull requests that close an item when every such item is already finished. The settle command for a pull request merged outside qew is documented.
