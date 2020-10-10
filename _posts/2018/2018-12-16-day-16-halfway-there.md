---
category: devlog
layout: post
tags:
- devember
- devember2018
- hourofcode
- raytracerchallenge
- ruby
title: Day 16, Halfway there
date: '2018-12-16T21:31:24+01:00'
---
Fitting that the halfway point would be about reflections. Pagewise we're more than halvway through the book, but I'm guessing that there will be plenty of things to do for the remaining 15 days. There's still the going back and replacing the [homebuilt algebra][] code with stdlib, if nothing else.

![Reflections](/img/2018/12/reflections.png){: .right }

Reflections is just another ray to cast, from the point of reflection, and see what it hits. Whatever the reflection ray hits is blended into the Phong lighting. Recurse until satisfied.

Currently the recursion is aborted after a fix number of steps, but I'm pondering if it would be better so let recursion run until the contribution is small enough not to matter, and set a much higher fixed limit. That way barely reflective surfaces wont waste computation, but higly reflective surfaces, like a mirror maze, get the best possible fidelity.

[homebuilt algebra]: /2018/12/02/day-2-matrices-matrices-matrices-oh-and-more-matrices/
