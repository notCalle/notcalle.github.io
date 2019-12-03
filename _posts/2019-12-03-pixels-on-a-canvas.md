---
layout: post
title: Pixels on a canvas
category:
- devlog
tags:
- devember
- devember2019
- hourofcode
- swift
- raytracing
date: 2019-12-03 23:06 +0100
---
Pretty much the whole point of a ray tracer such as this one is to render pretty pictures, and for that we're going to need a canvas to render onto.

```swift
typedef Pixel = simd_float4

struct Canvas { let width: Int; let height: Int }
```

Pixels can be set on the canvas, and it can be inspected to see what's already there. When the rendering is complete the canvas can be exported for display or file output.
