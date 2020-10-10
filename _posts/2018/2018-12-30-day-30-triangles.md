---
category: devlog
layout: post
tags:
- devember
- devember2018
- hourofcode
- raytracerchallenge
- ruby
title: Day 30, Triangles and teapots
date: '2018-12-30T22:53:03+01:00'
---
![Utah teapot](/img/2018/12/teapot.png){: .right }
The last of the primitive shapes, the triangle. By them selves they're pretty boring, but when you stick loads of them together they make pretty teapots. Very. Slowly. And quite chunky, because low-polygon model. It sums up to 240 triangles after dividing some larger polygons, and takes about 20–30 minutes to render at the whopping resulution of 320x256 and no reflections. I probably need to research some kind of [bounding hierarchy][] algorithm to automagically subdivide large groups of objects.

[bounding hierarchy]: https://en.wikipedia.org/wiki/Bounding_interval_hierarchy