---
layout: post
title: Hyperfixation Revisited
follows: /2020/09/30/hyperfixation
category: discord
tags:
- adhd
- scss
- jekyll
---
![overflow]{:.left.max50}
For some reason I found myself browsing my old blog posts, when I got assaulted by this scene, as straight out of a horror movie.

And while I was adding `@extend %clearfix` in places, I also thought I'd fix some other layout imperfections I noticed, and all of my morning disappeared; time to make coffee and "go to" work.

### Down the rabbit hole again

This was also the first time I've made a follow-up to a specific post, instead of referencing earlier posts in a series on a given theme, so I needed to make that kind of relation stand out.

While doing this, I had found horrible abuses of `<ul>` and `<li>` wrappers for vertical layout, so I ripped those out and flattened the DOM tree a bit. With this the actual blog post got promoted to be the main content, instead of just another list item with the related posts, so that's nice.

Now I've started thinking, and I should take a look at making a light theme for those who have not yet embraced the darkness; so investingation of media queries for that, and switch to using [custom CSS properties] instead of SASS variables for the color theme. That way I can wrap the color theme setup in a media query to get automatic switching, depending on the viewer's preference.

[overflow]: /img/2021/css-overflow.png "Floating image extending outside its container"
[custom CSS properties]: https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties
