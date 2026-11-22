id: 044yym12e
kind: issue
title: Track the core and graphql rate limits separately
parent: 044yyj516
needs: 
labels: 
owner: 
priority: 2
created: 2026-11-22T21:27:16Z
evidence: ymvzwzxk sssqknwl vssnzzun ymxkxlvw
---
## Problem

a GraphQL answer carrying its own x-ratelimit headers overwrites the REST accounting the background reserve and pr migrate read.

## Done when

WATCH is kept per resource, the reserve holds on the resource a request uses
