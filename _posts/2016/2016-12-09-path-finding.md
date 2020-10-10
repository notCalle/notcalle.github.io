---
layout: post
title: Path Finding
category: devlog
tags:
- devember
- devember2016
- swift
- xcode
date: '2016-12-09T23:27:35-05:00'
---
First attempt at using the `GamePlayKit` path finding `GKGridGraph`. Unfortunately, the playground currently crashes (because of some internal *XCode* bug maybe?), so it can't be tested.

The idea is that an actor can move if there is something present on the layer directly below them, but can't move through layers they occupy themselves. Currently hardcoded as requirement for tiles on `region.layers[0]` but this environment evaluation should probably be a method of the actor, as e.g. flying or swimming actors might have other ideas. Also, the graph generation should be restricted to what an actor has actually see, so they can't figure out a perfect path through unknown terrain.