---
layout: post
title: Directional Navigation
category: devlog
tags:
- devember
- devember2016
- swift
date: '2016-12-07T08:05:41-05:00'
---
Prereq work for implementing path finding: eight direction navigation. A tile can find its neighbours within its layer `exit(direction:)`. Currently only within a single map region, because we haven't implemented interregion links yet.