---
layout: post
title: Messy shadows
category:
- devlog
tags:
- devember
- devember2019
- hourofcode
- swift
- raytracing
date: 2019-12-08 22:14 +0100
---
Apparently, I messed up some more vector algebra. Ray / surface hits currently record the event in surface space, which works just fine for shading a unit sphere still positioned at origin. When we transform things around, and try to cast the secondary shadow rays, it becomes painfully obvious that surface space and world space no longer coincide.

![Messed up shadows](/img/2019/12/messy-shadows.png)
