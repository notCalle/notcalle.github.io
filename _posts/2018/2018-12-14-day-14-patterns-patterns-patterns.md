---
category: devlog
layout: post
tags:
- devember
- devember2018
- hourofcode
- raytracerchallenge
- ruby
title: Day 14, Patterns, patterns, patterns
date: '2018-12-14T21:16:51+01:00'
---
![Big Stripey Truth](/img/2018/12/big-stripey-truth.png){: .right }
![All the patterns](/img/2018/12/all-the-patterns.png){: .right }

The more, the merrier, they say, and that probably goes for patterns as well. Stripes got some more company, with gradients, concentric circles, and checkered patterns. And why constrain the number of colors in a pattern?

```ruby
def color_at(point)
  g = grade(point)
  c = @pigments.count - 1
  p = g.floor % c
  a, b = @pigments[p..p + 1]
  a.interpolate(b, g % 1)
end
```

Most of the work getting the multicolor working was refactoring all the kinds of patterns I created before. Each kind of pattern implements their own version of the `grade` method, that converts a 3D point to a scalar value, and the the base class takes care of the rest. With that in place, extending patterns to taking other patterns as pigments, instead of just plain colors, should be an easy next step.

{: .clear }
_Discrete rings_
```ruby
def grade(point)
  Math.sqrt(point.x**2 + point.z**2).floor
end
```

{: .clear }
_Linear gradient_
```ruby
def grade(point)
  point.x
end
```