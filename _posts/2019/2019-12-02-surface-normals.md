---
layout: post
title: Surface normals
category:
- devlog
tags:
- devember
- devember2019
- hourofcode
- swift
- raytracing
date: 2019-12-02 18:37 +0100
---
Today brings [normal vectors] into the mix, a critical component for shading computations; the normal vector of a surface at the point where it was hit by a ray, to be precise. Because the normal depends on the hit position on the surface, and we'll need that too, we keep that around as well.

```swift
struct Hit { let surface: Surface; let position: Point; let normal: Vector }

extension Ray { func hit(Surface) -> Hit? }
```

For the (2-dimensional) [unit sphere], our only surface so far, the normal at a point on its surface can be calculated as the vector from origin: $$\overrightarrow{N}_{hit} = \dot{P}_{hit} - \dot{0}$$

[normal vectors]: https://en.wikipedia.org/wiki/Normal_(geometry)
[unit sphere]: https://en.wikipedia.org/wiki/Unit_sphere
