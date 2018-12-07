---
category: devlog
layout: post
tags:
- devember
- devember2018
- hourofcode
- raytracerchallenge
title: Day 7, Casting rays through the whole world
---
Lots of refactoring happened today, because old assumptions were smashed, and some cleanup of annoying duplications was needed. No new pixels yet, but maybe tomorrow?

Casting a ray through the world is as simple as casting it through every object in the world, and collating the resulting intersections.
