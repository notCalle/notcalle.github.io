---
category: devlog
layout: post
tags:
- devember
- devember2018
- hourofcode
- raytracerchallenge
title: Day 7, Casting rays through the whole world
date: '2018-12-07T21:41:39+01:00'
---
Lots of refactoring today, because old assumptions were smashed, and some cleanup of annoying duplications was needed. No new pixels yet, but maybe tomorrow? These where the previous two days pixel results, with the black background made transparent while converting them from `ppm` to `png`.

![Flat Sphere](/img/2018/12/sphere.png)
![Phong Sphere](/img/2018/12/lit-sphere.png)

Casting a ray through the world is as simple as casting it through every object in the world, and collating the resulting intersections.
