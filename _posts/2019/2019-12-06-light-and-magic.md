---
layout: post
title: Light and Magic
category:
- devlog
tags:
- devember
- devember2019
- hourofcode
- swift
- raytracing
date: 2019-12-06 22:32 +0100
---
The next natural step after getting basic shading to work is to have actual light sources, that can be tinted and positioned in the scene.

Enter the `PointLight()` and `DistantLight()` classes of lights. A point light can be translated to a position, and irradiates the scene spherically from that position, and will be attenuated by distance. A distant light on the other hand, irradiates the scene with parallel rays of light, with the same power, and direction all over (like the fake "camera light").

Because we can't have more than one surface in the world at the moment, nothing can obscure the light (cast shadows). Here we have three light sources, yellow above to the left, cyan above to the right, and magenta below in front.

![Light & Magic](/img/2019/12/light-and-magic.png)
