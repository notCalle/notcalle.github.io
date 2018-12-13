---
category: devlog
layout: post
tags:
- devember
- devember2018
- hourofcode
- raytracerchallenge
- ruby
title: Day 13, Big Stripey Lie
date: '2018-12-14T00:14:12+01:00'
---
![Big Stripey Lie](/img/2018/12/big-stripey-lie.png){: .right }

Single color objects are boring, so some color patterns would be a nice addition. Like stripes, alternating between two colors, `a` and `b`.

```ruby
def color_at(point)
  (point.x.floor % 2).zero? ? @a : @b
end
```

{: .clear }

![Big Stripey Truth](/img/2018/12/big-stripey-truth.png){: .left }

Ok, uniform stripes all over the world is not the best thing, so they need to have transforms attached, like everything else. That's more like it.

```ruby
def color_at_object(object, point)
  object_point = object.inverse * point
  pattern_point = @inverse * object_point
  color_at(pattern_point)
end
```
