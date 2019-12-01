---
layout: post
title: Basic data types
category:
- devlog
tags:
- devember
- devember2019
- hourofcode
- swift
date: 2019-12-01 11:29 +0100
---
Alright, the first push to the [github repo] is complete. Starting out small with just the basic data types that will be at the core of everything, and some tolerance equality operators for comparisons.

The constructor functions `point()` and `vector()` use the neat trick of tagging with `.w = 1.0` for Points and `.w = 0.0` for Vectors.

```swift
typealias Point = simd_double4
typealias Vector = simd_double4
struct Ray { let origin: Point; let direction: Vector }

let r = Ray(origin: point(0,0,0), direction: vector(1,1,1))
r.direction ==~ vector(sqrt(1/3)) // rays have normalized direction
```

On a side note, I'm trying out the [pomodoro technique] to manage my ability to focus for this project; working in sets of 25 minutes, and taking 5 minute breaks. Maybe I should rephrase the Devember contract as I will work for two pomodoros per day, instead of one hour. Plus one pomodoro for the devlog.

[Github repo]: https://github.com/notCalle/swift-raytrace.git
[Pomodoro Technique]: https://en.wikipedia.org/wiki/Pomodoro_Technique
