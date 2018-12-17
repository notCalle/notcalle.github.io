---
category: devlog
layout: post
tags:
- devember
- devember2018
- hourofcode
- raytracerchallenge
- ruby
title: Day 17, Transparency and Refraction
date: '2018-12-17T23:43:32+01:00'
---
No new pixels today, because implementing transparency and refraction turned out to be quite a lot of work. So far I've made all the cases where nothing happens, and the refracted ray would be black.

  1. The material is not transparent (trivially)
  2. The maximum recursion depth is reached and search is aborted
  3. Total internal reflection would lead to 2, but is detected early

The next step, for tomorrow, should be about finding an actual color, and viewing the world through refractive distortions.
