---
layout: post
title: Intersecting spheres
category:
- devlog
tags:
- devember
- devember2019
- hourofcode
- swift
- raytracing
date: 2019-12-01 18:19 +0100
---
The first piece of actual ray tracing: calculating the [intersection between a ray and a sphere]. To find the intersections, we need to solve the quadratic equation of the sphere being equal to the linear equation of the ray. The interpretation of imaginary roots is that the ray does not intersect the sphere.

Combining the sphere equation $$\|\dot{x} - \dot{C}\|^2 = R^2$$ and the line equation $$\dot{x} = \dot{O} + t\overrightarrow{D}$$ we get:

$$\|\dot{O} + t\overrightarrow{D} - \dot{C}\|^2 = R^2$$

Since the unit sphere is centered at $$\dot{0}$$ and its radius is $$1$$, the equation can be simplified:

$$\|\dot{O} + t\overrightarrow{D}\|^2 - 1 = 0$$

[intersection between a ray and a sphere]: https://en.wikipedia.org/wiki/Line–sphere_intersection

_On another pomodorian side note, actually taking the 5 minute breaks every 25 minutes is really hard, but I'm starting to see how it might be worth it, by not falling into a hyperfocus trance until suddenly SO HANGRY AND WHERE DID THE DAY GO?!_
