---
category: devlog
layout: post
tags:
- devember
- devember2018
- hourofcode
- raytracerchallenge
- ruby
title: Day 10, A world full of spheres
date: '2018-12-10T17:48:40+01:00'
---
With the development environment fixed, using the previous progress to render a world with multiple is as simple as creating the camera:

```ruby
camera = Camera.new(128, 128, '1/4'.to_r) do |camera|
    origin = Point[0, 0, -1.7]
    look_at = Point[0, 0, 0]
    up = Vector[0, 1, 0]
    camera.transform = ViewTransform[origin, look_at, up]
end
```

Populating a world with some objects:

```ruby
world = World.new do |world|
    world.objects << Sphere.new do |sphere|
        sphere.material.color = Color[1, 0.3, 0.1]
        sphere.transform = identity.translate(-0.5, -0.5, 0)
    end
    world.objects << Sphere.new do |sphere|
        sphere.material.color = Color[1, 1.0, 0.1]
        sphere.material.shininess = 20
        sphere.transform = identity.translate(1, 1, 1)
    end
    world.objects << Sphere.new do |sphere|
        sphere.material.color = Color[0.2, 0.5, 1.0]
        sphere.transform = identity.scale(2, 2, 2).translate(-2, 2, 4)
    end
end
```

And finally rendering the result to an image file.

```ruby
File.open('spheres.ppm', 'w') do |file|
    camera.render(world).to_ppm(file)
end
```

![Spheres](/img/2018/12/spheres.png)
