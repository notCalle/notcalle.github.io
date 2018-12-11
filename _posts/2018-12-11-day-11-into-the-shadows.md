---
category: devlog
layout: post
tags:
- devember
- devember2018
- hourofcode
- raytracerchallenge
- ruby
title: Day 11, Into the Shadows
date: '2018-12-11T22:03:54+01:00'
---
After todays work we can render the shadows cast by objects in our scenes!

Finding out which points are in shadow is actually pretty neat, just cast a ray toward the light, and see if it hits anything else on the way. If the light is obscured, the point just gets ambiant light. When lit by multiple lights, the whole thing is just done separately for each light, and added in the end.

![Cornered Spheres](/img/2018/12/corner-spheres.png)
![Spheres with Shadows](/img/2018/12/sphere-shadows.png)
![Multi-light Shadows](/img/2018/12/multi-shadow-spheres.png)
