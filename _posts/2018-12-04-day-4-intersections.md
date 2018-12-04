---
category: devlog
layout: post
tags:
- devember
- devember2018
- hourofcode
- raytracerchallenge
title: Day 4, Intersections
date: '2018-12-04T23:34:42+01:00'
---
More math heavy stuff, calculating the positions along a ray, where it intersects a sphere. Turns out this is as simple as solving a quadratic equation, with some special coefficients. I'll need to come back and edit this with some formulae when I've befriended MathJax.

```ruby
def intersect(ray)
  sphere_to_ray = ray.origin - @origin
  a = ray.direction.dot(ray.direction)
  b = 2 * ray.direction.dot(sphere_to_ray)
  c = sphere_to_ray.dot(sphere_to_ray) - @radius_squared

  intersections = quadratic(a, b, c).map { |t| Intersection.new(t, self) }
  Intersections.new(*intersections)
end
```

I also had to refactor the symbolic evaluation helpers I use to evaluate the [gherkin][] expressions that makes up the specification.

```ruby
def seval(recv, method = nil, *args)
  case method
  when :'='
    instance_variable_set(recv, seval(*args))
  when nil
    recv.is_a?(Symbol) ? instance_variable_get(recv) : recv
  else
    fcall(map_operator(method), recv, *args)
  end
end

def fcall(method, *args)
  method.to_proc.call(*args.map do |arg|
    arg.is_a?(Symbol) ? instance_variable_get(arg) : arg
  end)
end
```

[gherkin]: https://docs.cucumber.io/gherkin/reference/
