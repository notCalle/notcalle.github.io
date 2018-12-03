---
category: devlog
layout: post
tags:
- devember
- devember2018
- hourofcode
- raytracerchallenge
- ruby
title: Day 3, Casting rays into spheres
date: '2018-12-03T23:30:11+01:00'
---
Finally some practical applications of the math heavy weekend, casting abstract rays at abstract spheres. Well, on a sliding scale from linear algebra to physical representation, it's still a step in the direction.

More reasonable pace, now that we've entered the workdays part of the week, with just an hour of coding-while-breakfast, that I didn't realize I had missed so much. It must have been during Devember 2016, while I was at a conference for a third of it, and because westward transatlantic jetlag was awake a few hours ahead of the conference schedule. I sat in the hotel lobby, eating expensive and not that good nuked oatmeal for breakfast, and working on my Devember project. That Devember project didn't work out, but that week was great.

Oh, back to [casting rays at spheres][]. I guess this can't stay around forever:

```ruby
class Sphere
  ...
  def intersect(_ray)
    raise NotImplementedError
  end
  ...
end
```

[casting rays at spheres]: https://en.wikipedia.org/wiki/Line–sphere_intersection
