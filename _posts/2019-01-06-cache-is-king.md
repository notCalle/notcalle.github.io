---
category: devlog
layout: post
tags:
- raytracerchallenge
- hourofcode
- ruby
title: Cache is King
date: '2019-01-06T20:46:24+01:00'
---
Cut teapot rendering time in half with some clever caching.

Grouped shapes would transform intersecting rays by first asking their parent to transform it, recursively until the outermost group is reached. This caused a lot of unneccessary 4x4 matrix multiplications. Instead, the shape creates a cached  world-to-local space transform by asking its parent for their world-to-local transform and multiplying by its own. Down to one 4x4 matrix multiplication per ray intersection test instead of the nesting depth of groups-within-groups.

Even worse, when transforming normal vectors for a hit recursively back to world space through all nested groups, there was not only an unneccessary 4x4 matrix multiplication, but also a vector normalization.

While I was at it I made sure that matrix operations on the identity matrix are actually no-ops, which shaved another 20% from the rendering time.
