---
category: devlog
layout: post
tags:
- raytracerchallenge
- ruby
title: Threaded rendering
date: '2019-01-13T00:21:39+01:00'
---
Shaved another 30% off rendering time by inlining and some more caching, but it seems like I'm reaching the limit of what I can get out of a single thread.

```pry
[1] pry(#<GlisteningRuby::DSL::Scene>)> render verbose:true
 Setup time: 0.532384 s
Render time: 259.392946 s
 Total time: 259.92533 s
```

There's quite a bit of overhead, because Ruby doesn't run its native threads in parallel, so we have to fork and return the result serialized via a file to the parent. This could probably be further optimized by not serializing as YAML, and reusing the render threads, but anyway.

```pry
[2] pry(#<GlisteningRuby::DSL::Scene>)> render verbose:true, threads:2
 Setup time: 0.522643 s
Render time: 149.411224 s
 Total time: 149.933867 s
```

This is the number of real CPU cores in my workstation.

```pry
[3] pry(#<GlisteningRuby::DSL::Scene>)> render verbose:true, threads:4
 Setup time: 0.580056 s
Render time: 85.895065 s
 Total time: 86.475121 s
```

Using hyperthreading quickly loses efficiency, but gets the CPU fan going.

```pry
[3] pry(#<GlisteningRuby::DSL::Scene>)> render verbose:true, threads:8
 Setup time: 0.560456 s
Render time: 77.613168 s
 Total time: 78.173624 s
```
