---
category: devlog
layout: post
tags:
- devember
- devember2018
- hourofcode
- raytracerchallenge
- ruby
title: Day 31, Optimizing triangles
date: '2018-12-31T12:19:26+01:00'
---
![Utah teapot in reflective room](/img/2018/12/teapot-reflection.png){: .right }
Triangle rendering was painfully slow, as mentioned [yesterday][]. Putting a little reflective shine on the floor and walls of the room took rendering time past 90 minutes. After a bit of research i tried a binary [bounding volume hierarchy][], dividing the list of shapes into subtrees, split evenly on the largest axis of the bounding box, recursively. This way we get a spacially balanced binary tree with the actual shapes as leaves, and theoretically get $$O(log\ n)$$ instead of $$O(n)$$ search time per ray. Huge difference, especially with rays branching recursively for reflections and refractions. Down from 90 to 6 minutes for the same scene.

This marks the end of Devember 2018, but there's still some more work to do on the raytracer before I let it go. The flat shading of triangles needs some normal interpolation, and the primitive volumes needs some [constructive solid geometry][] operations to really shine.

[yesterday]: /2018/12/30/day-30-triangles/
[bounding volume hierarchy]: https://en.wikipedia.org/wiki/Bounding_volume_hierarchy
[constructive solid geometry]: https://en.wikipedia.org/wiki/Constructive_solid_geometry
