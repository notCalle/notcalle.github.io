---
category: devlog
layout: post
tags:
- raytracerchallenge
- ruby
title: Soft Shadows
date: '2019-01-29T23:04:59+01:00'
---
![Hard shadows](/img/2019/01/teapot-hardshadow.png){: .right }
With the recent anti-aliasing feature enables, the image quality is pretty good, but the shadow edges are still too hard to be realistic, because the light source is still just a point without surface area.

{: .clear }
```pry
[1] pry(#<GlisteningRuby::DSL::Scene>)> render verbose:true, threads:8, ssaa:3
 Setup time: 0.574395 s
Render time: 554.427143 s
 Total time: 555.001538 s
```

![Soft shadows](/img/2019/01/teapot-softshadow.png){: .right }
We can simulate a light source with a surface area by giving the spherical point light a radius. When the radius is zero, it behaves as before, but when it has a non-zero radius, we cast multiple random shadow rays towards the spherical light volume, and average the result. Combined with SSAA everything looks perfectly smooth.

{: .clear }
```pry
[1] pry(#<GlisteningRuby::DSL::Scene>)> render verbose:true, threads:8, ssaa:3
 Setup time: 0.563097 s
Render time: 1501.46532 s
 Total time: 1502.028417 s
```

To manage rendering time, the number of shadow rays is dynamic, with primary ray intersections casting the most number of samples, and rapid falloff over recursion into reflection and refraction. The number of samples is also proportional to the apparent size of the light source at the point of intersection.

Currently the whole scene is intersected for each shadow ray sample, but it should be possible to select a set of possible intersection candidates and multisample against that reduced set instead.
