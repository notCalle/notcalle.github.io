---
date: 2016-08-22T23:44:14+02:00
layout: post
title: XCode build number from git
category: devlog
tags:
- xcode
---
Add this as a **Run Script Phase** at the end of **Build Phases** in your XCode project to increment your CFBundleVersion as *{git commit count}.{uncommitted changes}-{gitrevid}*.

{% gist notCalle/af53a0b3ccac6123c8a2d2337a48dc6a %}

When the build is made from a cleanly committed git repository the version will be N.0-XXXXXXX. Intermediary test builds will have N.D-XXXXXXX with the size of the diff from the actual committed version as minor.
