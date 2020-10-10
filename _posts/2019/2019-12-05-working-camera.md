---
layout: post
title: Working camera
category:
- devlog
tags:
- devember
- devember2019
- hourofcode
- swift
- raytracing
date: 2019-12-05 20:21 +0100
---
So yesterday's attempt at capturing an image didn't turn out so well, because I messed up the camera, or rather the vector algebra behind everything. When I realized what I had done, I instantly remembered that similar lesson from last year; because points have `w=1`, while vectors have `w=0`, almost all vector operations will get messed up by the extra `1`, if you accidentally use a point instead. Or vice versa.

When fixing that I also realized I forgot to translate the camera away from the origin of the sphere I tried to take a picture of, but the vector/point mess-up had accidentally warped space to get a decent composition anyway.

```swift
typealias Transform = simd_double4x4

extension Transform {
    static func translate(to position: Point) -> Transform {
        simd_matrix(.vector(1,0,0),
                    .vector(0,1,0),
                    .vector(0,0,1),
                    position)
    }
}
```

And with that, the "camera light" shaded sphere is rendered at full intensity.

![White sphere](/img/2019/12/white-sphere.png)
