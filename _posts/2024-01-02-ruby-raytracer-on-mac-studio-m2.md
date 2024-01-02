---
layout: post
title: Ruby Raytracer on M2 Max
date: 2024-01-02 22:48 +0100
follows: /2022/05/11/ruby-raytracer-on-m1
tags:
- raytracerchallenge
- raytracing
- ruby
category: discord
---
A few years — and iterations of the _Apple M-series_ — has passed, and I recently found myself in possession of a _Mac Studio M2_, in its base configuration of _8P + 4E_ CPU cores, and even more ridiculous[^1] amounts of cache.

[^1]: This monster has 87 MiB L1+L2+L3 cache in total. _It can fit my entire first hard-drive (52 MB) in CPU cache._

But the burning question is, does it deliver on the promise of up to 18% CPU speed improvement?

### Hard shadows

The base-line benchmark, as before, is the single-threaded render without any fancy rendering techniques active

###### Mac Studio M2 (2023)

```pry
[1] pry(#<GlisteningRuby::DSL::Scene>)> render verbose:true
 Setup time: 0.178938 s
Render time: 104.306864 s
 Total time: 104.485802 s
```

That's a 17% improvement in single-core performance over the M1, so right on the spot.

###### MacBook Pro M1 (2021)

```pry
[1] pry(#<GlisteningRuby::DSL::Scene>)> render verbose:true
 Setup time: 0.240659 s
Render time: 122.153057 s
 Total time: 122.393716 s
```

Then we get into the unfair territory, because the M1 did the multi-threaded benchmark using all its P-, and E-cores, where the M2 Max can let its P-cores do all the work.

###### Mac Studio M2 (2023)

```pry
[1] pry(#<GlisteningRuby::DSL::Scene>)> render verbose:true, threads:8
 Setup time: 0.173121 s
Render time: 15.689671 s
 Total time: 15.862792 s
```

**BOOM** even lightning faster — over six and a half times as fast multi-threaded, and almost twice (1.79x) as fast as the M1 was.

###### MacBook Pro M1 (2021)

```pry
[2] pry(#<GlisteningRuby::DSL::Scene>)> render verbose:true, threads:8
 Setup time: 0.266847 s
Render time: 28.061283 s
 Total time: 28.32813 s
```

### Going All In — Soft Shadows and Anti-Aliasing

This time, we're throwing everything we have, letting the tiny E-cores do what they can to help along.

###### Mac Studio M2 (2023)

```pry
[1] pry(#<GlisteningRuby::DSL::Scene>)> render verbose:true, threads:12, ssaa:3
 Setup time: 0.17466 s
Render time: 304.752032 s
 Total time: 304.926692 s
```

Just shy of twice (1.97x) the crunch of an M1, in the extremely unfair final round.

###### MacBook Pro M1 (2021)

```pry
[1] pry(#<GlisteningRuby::DSL::Scene>)> render verbose:true, threads:8, ssaa:3
 Setup time: 0.23379 s
Render time: 601.335931 s
 Total time: 601.569721 s
```

Still, this is an extremely inefficient raytracer, and nothing we can throw at it will make renders reasonable. All the benchmarks yield a 320x256 image, which of course is the standard Amiga PAL low-res, and would take days to run with an optimized raytracer on an actual Amiga.

Which raises the next question, is it more efficient to emulate an Amiga, running an optimized raytracer, than this nonsense one I made in Ruby?
