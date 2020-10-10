---
category: devlog
layout: post
tags:
- devember
- devember2018
- hourofcode
- ruby
- raytracerchallenge
- tauism
title: Day 2, Matrices, matrices, matrices. Oh, and more matrices
date: '2018-12-02T23:45:24+01:00'
---
Today was spent on a heavy chunk of [linear algebra][], matrices. This is the foundation for everything else, so time well spent reimplementing what's already in the stdlib, just to refresh my math skills. If there are still days left of Devember when I'm finished, I'll come back and replace all this with the stdlib implementation instead, hoping I'm somewhat close to the same API.

The next natural step, was defining the different transformations needed for all vector space calculations, and also happened to be the next chapter in the book.

Now we're almost ready for some real action.

```ruby
p = Point[0, 1, 0]
T = identity.rotate_x(0.25) # We're counting rotation in units of τ
T * p
=> (0.0, 0.0, 1.0, 1.0)
```

[linear algebra]: https://en.wikipedia.org/wiki/Linear_algebra
