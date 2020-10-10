---
category: devlog
layout: post
tags:
- raytracerchallenge
- ruby
title: Super Sampling Anti-Aliasing
date: '2019-01-13T11:35:32+01:00'
---
![Jaggy Utah Teapot](/img/2019/01/teapot-jaggies.png){: .right }
Remember the smoothly shaded teapot? Still looks pretty rough with all the jaggies and speckles. Well, with the shiny new [multi threading][] support it's actually feasible to add some image quality improvements.

{: .clear }
```pry
[1] pry(#<GlisteningRuby::DSL::Scene>)> render verbose:true, threads:8
 Setup time: 0.564666 s
Render time: 73.976052 s
 Total time: 74.540718 s
```

![Smooth Utah Teapot](/img/2019/01/teapot-ssaax3.png){: .right }
Same scene, but rendered with 3x Super Sampling Anti-Aliasing. Nine times as many rays to cast into the world should mean nine times as long rendering time, but the good news is that with heavier rendering, the threading overhead is offset slightly so we only pay 7.5x time penalty for 9x processing.

{: .clear }
```pry
[2] pry(#<GlisteningRuby::DSL::Scene>)> render verbose:true, threads:8, ssaa:3
 Setup time: 0.5425 s
Render time: 561.85829 s
 Total time: 562.40079 s
```

[multi threading]:/2019/01/13/threaded-rendering/
