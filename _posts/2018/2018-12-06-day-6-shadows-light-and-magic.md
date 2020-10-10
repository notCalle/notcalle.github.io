---
category: devlog
layout: post
tags:
- devember
- devember2018
- hourofcode
- raytracerchallenge
- ruby
title: Day 6, Shadows, Light and Magic
date: '2018-12-06T09:19:12+01:00'
---
More than just hit detection, we've moved into the realm of reflection, lighting and shading. This is mainly about projecting vectors on other vectors, using dot products $$\overrightarrow{v1} \cdot \overrightarrow{v2}$$ to measure the length of the projection. For that we need to find normal vectors of surfaces, and a light source.

The point light source is simple enough, just a position and an intensity.

$$
light = (\dot{p}, i_{rgb})
$$

The [normal][] at a point of a unit sphere is also simple, it's the same as the vector from the center to the point on the sphere.

$$
\overrightarrow{v}_{normal} = \dot{p}_{sphere} - \dot{p}_{origin}
$$

That's in object space. The actual calculation in world space is a bit more convoluted, because we have transforms attached to the unit spheres, so a few inverse transforms are needed to counter the deformation.

```ruby
def normal_at(world_point)
  object_point = @inverse * world_point
  object_normal = object_point - Point::ZERO
  world_normal = @inverse_transpose * object_normal
  world_normal.normalize
end
```

With that in place we can calculate the shade where the ray hits a sphere, by using the [Phong reflection][] model.

[normal]: https://en.wikipedia.org/wiki/Normal_(geometry)
[Phong reflection]: https://en.wikipedia.org/wiki/Phong_reflection_model
