---
category: devlog
layout: post
tags:
- devember
- devember2018
- raytracerchallenge
- hourofcode
- ruby
title: Day 36, Constructive Solid Geometry
date: '2019-01-05T13:05:22+01:00'
---
The final pre-defined feature of the project is done, [Constructive Solid Geometry][], implementing the boolean set operations `union`, `intersection`, and `difference` for solid geometries. This way we can use the basic geometric surface shapes to create more advanced shapes, without resorting to approximating by thousands of triangles.

{: .clear }
![Union](/img/2019/01/csg-union.png){: .left }
The CSG union operation joins the surface of two shapes, such that the outer geometry is preserved, but the overlapping geometry on the inside is removed, constructing a new surface.

{: .clear }
![Intersection](/img/2019/01/csg-intersection.png){: .left }
The CSG intersection operation does the opposite of the union, preserving only the overlapping geometry. That's why the colors switch sides, because the remaining surface geometries belong to the opposite side spheres.

{: .clear }
![Difference](/img/2019/01/csg-difference.png){: .left }
The last of the operations, CSG difference, removes the intersection from the left sphere, again leaving the surface of the right sphere exposed in the cut.

{: .clear }
![Dice](/img/2019/01/dice.png){: .right }
With some clever arrangement of CSG operations we can create some pretty complex geometry from just some cylinders and spheres.

[Constructive Solid Geometry]: https://en.wikipedia.org/wiki/Constructive_solid_geometry
