---
layout: post
title: RasPi 400 bonus benchmarks
follows: /2022/05/11/ruby-raytracer-on-m1
tags:
- raytracerchallenge
- raytracing
- ruby
date: 2022-05-12 20:34 +0200
category: discord
---
I didn't quite finish the bonus benchmarks, so for the sake of completeness,
here we go. The missing ones for the _RasPi 400_.

### Hard shadows

The Raspi only got a chance to show off with the heaviest of the benchmarks,
so let's see how it does in the lower end of teapot image quality.

###### Raspberry Pi 400 OC 2.2GHz (single threaded)

Single threaded performance still tracks at about the same ratio of _1/9 M1_.

```pry
[1] pry(#<GlisteningRuby::DSL::Scene>)> render verbose:true
 Setup time: 1.375927773 s
Render time: 852.156157512 s
 Total time: 853.532085285 s
```

###### Raspberry Pi 400 OC 2.2GHz (multi-threaded)

This one would seem a bit unfair, because the _RasPi 400_ only gets 4 threads
to do the work, instead of 8 threads for the other ones.

```pry
[2] pry(#<GlisteningRuby::DSL::Scene>)> render verbose:true, threads:4
 Setup time: 1.379623305 s
Render time: 292.012566677 s
 Total time: 293.392189982 s
```

The huge falloff in performance for those last 4 threads shows pretty clearly
here. The _RasPi 400_ performance/thread scales pretty well at _3/4_, given
the huge overhead of the threaded renderer, but the _M1_ only did _4/8_, and
the _i7_ was even worse with _3/8_.

Still, _4x M1_ is more than _3x RasPi 400_, so the total
performance ratio when using every single bit of crunch there is, is less
than _1/10 M1_.

More interesting is that the _RasPi 400_ did the soft-shadows render at only
_19x_ the time for hard-shadows, but the _M1_ took more than _21x_ the
time. The passive thermal design of the _RasPi 400_ continues to amaze me,
especially given the long history of overheated pies.
