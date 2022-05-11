---
layout: post
title: Ruby raytracer on M1
follows: "/2019/01/13/threaded-rendering"
tags:
- raytracerchallenge
- raytracing
- ruby
date: 2022-05-11 22:52 +0200
---
While doing something else than I was planning to, I accedentally came back to
the raytracer I once wrote in Ruby, and decided that the important thing just
now is to benchmark my _MacBook Pro M1_ against those old results. I guess
this will actually be _Ruby 3 on M1_ vs _Ruby 2 on i7_, because time happened.


### Single-threaded

Starting out with the single threaded teapot rendering benchmark. This should
give a pretty good measure of raw performance.


###### MacBook Pro M1 (2021)

```pry
[1] pry(#<GlisteningRuby::DSL::Scene>)> render verbose:true
 Setup time: 0.272459 s
Render time: 354.255657 s
 Total time: 354.528116 s
```


###### iMac i7 (2012)

```pry
[1] pry(#<GlisteningRuby::DSL::Scene>)> render verbose:true
 Setup time: 0.532384 s
Render time: 259.392946 s
 Total time: 259.92533 s
```

But wait? Setup time is twice as fast, but rendering is 30% slower? To quote
Arueshalae, _something is not right here._


### Multi-threaded

This the one that made the i7 melt, without providing much more pixels per
second than at half the threads. Let's see how the M1 fares here. Both have
about the same capacity of maximum performance threads, and the same total
level of parallelism. _4C + 4c_ vs _4C * 2T_.


###### MacBook Pro M1 (2021)

```pry
[2] pry(#<GlisteningRuby::DSL::Scene>)> render verbose:true, threads:8
 Setup time: 0.261933 s
Render time: 70.432901 s
 Total time: 70.694834 s
```

So, render time is about 1/5 of single-threaded. With the highly suboptimal
implementation, I guess this is about as good as can be expected. I think this
was the first time I could actually hear the CPU fan, in the year I've had
this machine.


###### iMac i7 (2012)

```pry
[3] pry(#<GlisteningRuby::DSL::Scene>)> render verbose:true, threads:8
 Setup time: 0.560456 s
Render time: 77.613168 s
 Total time: 78.173624 s
```

Now we're suddenly doing better than the i7, but that might be due to
thermal throttling? Could also be that the "efficiency" cores add more crunch
to the mix than the hyperthreads did.

Still, the setup — [building the Kd-tree] — is twice as fast. This does not add up.

[building the Kd-tree]: /2018/12/31/day-31-optimizing-triangles/


### Face palm

Those earlier benchmarks were run after all the primary optimizations had been
made, but before all the extra — performance draining — render quality
features were added.

Like soft shadows.

All. Those. Shadow. Rays. The Shadow? **The Shadow!** Rays!

Easily fixed, just adjust the spherical light source to point size, and all
those extra shadow rays goes away.


### Hard shadows

There we go; twice as fast single-threaded rendering.

```pry
[1] pry(#<GlisteningRuby::DSL::Scene>)> render verbose:true
 Setup time: 0.240659 s
Render time: 122.153057 s
 Total time: 122.393716 s
```

**BOOM** lightning fast — almost thrice as fast multi-threaded

```pry
[2] pry(#<GlisteningRuby::DSL::Scene>)> render verbose:true, threads:8
 Setup time: 0.266847 s
Render time: 28.061283 s
 Total time: 28.32813 s
```

Mystery solved, but where's the fun in stopping now?


### Going All In — Soft Shadows and Anti-Aliasing

The [final original benchmark] was rendering soft shadows with velvet smooth
anti-aliasing, so let's do that too, while we're here.

[final original benchmark]: /2019/01/29/soft-shadows/


###### MacBook Pro M1 (2021)

This time we might have hit the thermal throttling of the M1 as well, because
the CPU fan is wheezing increasingly louder, and the hand rest is getting warm
and toasty like you'd want when coming home on a cold winter night.

```pry
[1] pry(#<GlisteningRuby::DSL::Scene>)> render verbose:true, threads:8, ssaa:3
 Setup time: 0.23379 s
Render time: 601.335931 s
 Total time: 601.569721 s
```


###### iMac i7 (2012)

This time we're only 2 1/2 times as fast on the M1, and by the sound and feel
of it, thermal throttling is very much in effect.

```pry
[1] pry(#<GlisteningRuby::DSL::Scene>)> render verbose:true, threads:8, ssaa:3
 Setup time: 0.563097 s
Render time: 1501.46532 s
 Total time: 1502.028417 s
```

But wait, there's more!


### My other computer is also an ARM

So, I bought two new computers last year. The other was a Raspberry Pi 400.

This is a 4 core passively cooled beast, but still running overclocked from
1.8GHz to 2.2GHz without breaking a sweat. For normal "heavy" use, like
running video streams from rC3 all day, that is.


###### Bonus: Raspberry Pi 400 OC 2.2GHz

Sitting steady at 66°C core temperature with 30% of the rendering done, and an
estimate of 2400s to go. This estimate will go up though, because the first
30% is the easy part.

```pry
[6] pry(#<GlisteningRuby::DSL::Scene>)> render verbose:true, threads:4, ssaa:3
 Setup time: 1.374378639 s
Render time: 5541.122792698 s
 Total time: 5542.497171337 s
```

There we go. The final results are in. M1 beats everything by far, as expected,
but the RPi400 is just 9 times slower, on passive cooling. Not warmer to the
touch after 1 1/2 hours of hard work, than the actively cooled M1 was after
10 minutes.
