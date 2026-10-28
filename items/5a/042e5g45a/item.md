id: 042e5g45a
kind: issue
title: sync --dry-run reports the creates a recreated forge repo needs
parent: 
needs: 
labels: 
owner: 
priority: 1
created: 2026-10-09T07:54:49Z
evidence: qruzozzuzwyx vzvsntvuwnkv
---
## Problem

qew sync --dry-run says nothing to sync when every mirrored issue is missing on the forge, because it compares only event ids and mirror files.

## Fix

A dry run reads the forge listing and reports the recreate it would perform.

## Done when

A walk empties the fake forge and the dry run lists create lines for every item.
