---
layout: post
title: GameplayKit A*?
category: devlog
tags:
- devember
- devember2016
- swift
date: '2016-12-08T08:25:11-05:00'
---
Let's try to use the builtin [A*](https://en.wikipedia.org/wiki/A*_search_algorithm) in GameplayKit, and see if it works for our current demands. 

This reminded me that nothing in the game API:s uses `CGPoint`, so everything has been changed to use `vector_int2` instead.