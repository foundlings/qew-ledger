id: 042e5g81a
kind: issue
title: A forge=missing divergence clears when the issue exists again
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-09T07:54:53Z
---
## Problem

exists forge=missing divergences stay open after the issue is recreated and a full pull sees it.

## Fix

A full pull drops an exists/missing divergence whose issue is present, noting it in the output.

## Done when

A walk shows the divergence gone after the issue returns, without qew resolve.
