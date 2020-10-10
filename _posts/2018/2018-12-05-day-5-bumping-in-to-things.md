---
category: devlog
layout: post
tags:
- devember
- devember2018
- hourofcode
- raytracerchallenge
- ruby
title: Day 5, Assume nothing
date: '2018-12-05T10:45:08+01:00'
---
_Today I Learned_ that I shouldn't have assumed the sphere would ever need to change from being a unit sphere, so intersecting gets even simpler:

$$\|\dot{O} + t\overrightarrow{D}\|^2 - 1 = 0$$

```ruby
def intersect(ray)
  l = ray.origin - Point::ZERO
  d = ray.direction
  a = d.dot(d)
  b = 2 * d.dot(l)
  c = l.dot(l) - 1

  intersections = quadratic(a, b, c).map { |t| Intersection.new(t, self) }
  Intersections.new(*intersections)
end
```

You might wonder why subtract the zero point from the ray origin. $$x - 0 = x$$, right? Wrong! $$\dot{p_1} - \dot{p_0} = \overrightarrow{v_1}$$, subtracting points yields a vector, due to that neat trick I mentioned on [the 0:th day][], and $$v_1 \cdot v_2$$ is only valid for vectors, not points.

See, a point has w = 1, and a vector has w = 0

$$
\begin{bmatrix}
x1 \\ y1 \\ z1 \\ 1
\end{bmatrix}
-
\begin{bmatrix}
x0 \\ y0 \\ z0 \\ 1
\end{bmatrix}
=
\begin{bmatrix}
x1 \\ y1 \\ z1 \\ 0
\end{bmatrix}
$$

Like ma~~gic~~th.

[the 0:th day]: /2018/11/30/day-0-tuple-basics/
