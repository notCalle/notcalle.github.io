---
layout: post
title: All the things
category:
- devlog
tags:
- devember
- devember2019
- hourofcode
- swift
- raytracing
date: 2019-12-07 12:22 +0100
---
One limitation so far was that there could only be one surface in a scene. To get past that, we add the `Group` meta-surface, that contains a number of surfaces, and intersects with rays on their behalf. To make this actually useful, surfaces also need transforms to translate them out of their shared origin.

To keep the simplified unit sphere intersection formula, the surface is not actually transformed, but instead the intersecting ray is inversely transformed to shift its frame of reference to the surface.

![Group of spheres](/img/2019/12/grouped-spheres.png)
