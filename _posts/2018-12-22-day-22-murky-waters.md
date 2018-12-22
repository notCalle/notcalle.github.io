---
category: devlog
layout: post
tags:
- devember
- devember2018
- hourofcode
- raytracerchallenge
- ruby
title: Day 22, Murky waters
date: '2018-12-22T22:40:42+01:00'
---
Remember when we [introduced shadows][]? Casting a ray towards the light and see if any object is in the way. Well, that's a huge shortcut, because transparent materials. Well, why not fix that by taking another huge shortcut, and add a toggle to exclude certain objects from shadow ray casting?

![Murky water](/img/2018/12/shadowatery-floor.png)
![Clear water](/img/2018/12/watery-floor.png)

[introduced shadows]: /2018/12/11/day-11-into-the-shadows/
