id: 042fxfb8p
kind: issue
title: project status fails on a board with a text field (value.name)
parent: 042fnqu4s
needs: 
labels: 
owner: 
priority: 2
created: 2026-10-10T05:00:11Z
---
Regression from 4.18.0 project fields work: the ProjectCards parser still read name only, so any board card holding a text value broke qew project status. Reported by Santa on foundlings project 2.
