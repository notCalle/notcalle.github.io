---
category: devlog
layout: post
tags:
- devember
- devember2018
- hourofcode
- raytracerchallenge
- ruby
title: Day 12, Spheres on a plane
date: '2018-12-12T23:08:18+01:00'
---
Spheres are nice and all, but we need more shapes to make the world go around. So, a little bit of refactoring to get most the juicy bits from spheres apply to every kind of shape, such as planes. So flat, and infinite.

See, the seemingly flat floor and walls used to be very flat spheres, and not planes at all.

![Spheres on a disc](/img/2018/12/spheres-on-a-disc.png)
![Spheres on a plane](/img/2018/12/spheres-on-a-plane.png)

While messing around with non-square aspect ratios, trying to capture the scene, I got bit by a nasty bug in the camera:

```ruby
def initialize(width, height, fov)
  aspect_ratio = width / height
```

The `width` and `height` of the camera is measured in canvas pixels, so they are integers, which caused an integer division when calculating the aspect ratio, with surprising results. Rational numbers to the resque:

```ruby
def initialize(width, height, fov)
  aspect_ratio = Rational(width, height)
```
