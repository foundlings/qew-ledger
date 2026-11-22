id: 044xws23m
kind: issue
title: setup_user reinstalls into the live venv: hooks that run meanwhile fail with ImportError
parent: 
needs: 
labels: 
owner: 
priority: 2
created: 2026-11-22T08:55:22Z
discovered_from: 044xjcigz
---
## Where

scripts/setup_user.py

## Problem

pip uninstalls the old qew then installs the new one in place; for those seconds the agent guard hook (and any qew call) imports a package that is absent or half copied (foundlings agent saw ImportError on sync_plan, retry worked; sync_plan.py was not renamed).

## Fix

Build the wheel first, install it with no deps in one short step, and keep the old package importable until the new files are in place; add a walk that runs the install while a hook loop imports qew.

## Done when

A walk shows no import failure while setup_user runs.
