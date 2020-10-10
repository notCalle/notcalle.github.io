---
category: devlog
layout: post
tags:
- raytracerchallenge
- ruby
- hourofcode
title: Light and Magic
date: '2019-01-08T20:31:49+01:00'
---
![Room with a Window](/img/2019/01/room-without-falloff.png){: .right }
Made some refinements to lighting. Originially there was only a point light without distance falloff, which is not an accurate light model in any case. The light inside the room lights the entire world, all the way to the horizon.

To improve on the situation I rewrote the light model from scratch, keeping the original point light as a wrapper for simplified testing of the shading model.

![Room with a Window](/img/2019/01/room-with-window.png){: .right }
Two new kinds of lights, a `parallel` light that simulates an infinitely distant light source, so the incoming light rays are perfectly parallel and only have a direction. The other is a `spherical` light, which is a positional light source that radiates spherically, so intensity falls off with distance.

While I was at it, I refactored bits of the object hierarchy to enable light sources to be transformed and grouped just like any other object in the scene, so we can make reusable lamps.

{: .clear }
```ruby
shape.group :ceiling_lamp do |lit = true|
  light.spherical { falloff 0.1 } if lit
  shape.sphere do
    scale 0.1
    material do
      color :white
      ambient 0.8
      diffuse 0
      phong 0
    end
    shadows false
  end
  shape.cylinder do
    material :shiny_metal
    scale 0.01, 1, 0.01
    translate 0, 0.1, 0
  end
end
```
