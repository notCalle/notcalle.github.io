---
layout: post
title: SpriteKit evolved
category: devlog
tags:
- devember
- devember2016
- spritekit
date: '2016-12-14T20:49:34+01:00'
---
While poking around, I saw an intriguing class named `SKTileMapNode`, and it turns out that `SpriteKit` has gained support for rectangular, isometric, and hexagonal tile maps since last year. Looks like I can drop all of the plans for `GridMapKit` and just use what's there in the SDK already. Maybe I'll still need some of it to implement the plans for hierarchical maps of different scale, e.g. *world map*, detailed *terrain maps*, and *building/dungeon maps*.

Oh, and there is new stuff in `GameplayKit` for creating *noise maps* as well. Almost everything I spent last *Devember* doing, and that I was planning to port to *Swift* this time around has since been implemented in the SDK. Time for major replanning, and reading up on documentation instead, to find what else there is that I don't have to write myself anymore.