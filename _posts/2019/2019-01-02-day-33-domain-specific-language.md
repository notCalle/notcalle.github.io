---
category: devlog
layout: post
tags:
- devember
- devember2018
- hourofcode
- raytracerchallenge
- ruby
title: Day 33, Domain-Specific Language
date: '2019-01-02T23:39:22+01:00'
---
Not a single feature improvement today, but instead a bit of quality of life improvements.

One of the great things about modern dynamic introspective languages is that it's very easy to create a [domain-specific language][] for a project like this, to make a scene description be less like pages of complicated code, and more like a reasonably fluent declarative description of the objects in the scene.

```ruby
material :glazed_ceramic do
  color rgb 1.0, 0.8, 0.5
  ambient 0.3
  diffuse 0.7
  phong 0.9, 300
  reflective 0.1
end

shape.mesh :utah_teapot do |version = 'hi'|
  file "teapot-#{version}.obj"
  material :glazed_ceramic
  rotate x: -1/4r
  scale 1/16r
end
```

The top-level declarations creates methods on the appropriate classes so they can be called by reference later on to create the concrete model objects dynamically, and does more or less the same as the previous raw API code:

```ruby
def setup_teapot(world, version)
  world << ObjFile.new(File.open(__dir__ + "/teapot-#{version}.obj")) do |g|
    g.transform = identity.rotate_x('-1/4'.to_r)
                          .scale('1/16'.to_r)
    g.material = Material.new do |m|
      m.color = Color[1.0, 0.8, 0.5]
      m.shininess = 300
      m.diffuse = 0.7
      m.ambient = 0.3
    end
  end
end
```

[domain-specific language]: https://en.wikipedia.org/wiki/Domain-specific_language
