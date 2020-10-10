---
category: devlog
layout: post
tags:
- devember
- devember2018
- hourofcode
- raytracerchallenge
- ruby
title: Day 15, Patterns all the way down
date: '2018-12-15T22:21:26+01:00'
---
![Nested Patterns](/img/2018/12/nested-patterns.png){: .right}

I heard you liked patterns, so how about some patterns within your patterns, so you can pattern while you pattern?

Supporting nesting of the already existing patterns was not that difficult, just make colors respond to `#color_at(point)` and make a recursive call in the base class.

```ruby
def color_at(point)
  point = to_local(point)
  g = grade(point)
  c = @pigments.count - 1
  n = g.floor % c
  a, b = @pigments[n..n + 1].map { |p| p.color_at(point) }
  a.interpolate(b, g % 1)
end
```

![Arithmetic Blending](/img/2018/12/arithmetic-blending.png)
![Geometric Blending](/img/2018/12/geometric-blending.png)

Blending arbitrary patterns with a function is just as easy, so here are the arithmethic, geometric, and quadratic mean blends of the stripy patterns nested in the checkers before. This overrides the `#color_at` method completely, and so does the next modifier pattern, as they have no base pattern on their own.

![Quadratic Blending](/img/2018/12/quadratic-blending.png)
![Perturbations](/img/2018/12/perturbed-pattern.png)

While we're at it, why not add a simplex noise perturbation as well for organic patterns.