---
layout: post
title: First of Devember
category: devlog
tags:
- devember
- devember2016
- xcode
date: '2016-12-01T23:02:17+01:00'
---
Not a single actual line of code written today, but development environment setup had to take priority. The way to manage Cocoa dependencies seems to be [Carthage](https://github.com/Carthage/Carthage), so lets use that for our first known dependency, namely a new framework that will hold all reusable parts of the map handling and navigation code. *Carthage* looks somewhat similar to *bundler* of Ruby fame, so that's nice.