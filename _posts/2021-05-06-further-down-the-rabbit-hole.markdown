---
title: Further down the rabbit hole
layout: post
category: discord
tags:
- adhd
- scss
---

### Hello darkness, my old friend
![](/img/2021/hello-darkness.png "web page with dark color scheme"){:.right.max25}

I woke up way too early, and couldn't go back to sleep. What better way to spend a few hours before regular wake-up time, than hacking sassy style sheets?

```scss
$brand-color: #F15A29;
$gray-color:  desaturate($brand-color, 85%);
```

All color theming is now rewritten to use custom CSS properties instead of SCSS variables, and just the definition of the properties are SCSS. For some reason the jekyll sassifier does not expand `$variable`{:.nowrap} in custom properties, so all those had to be wrapped in `#{$variable}`{:.nowrap} interpolations instead.

{:.clear}
```scss
$dark-gray-color:           $gray-color;
$dark-background-color:     darken($dark-gray-color, 45%);
$dark-text-color:           lighten($dark-gray-color, 40%);

:root {
    --base-bg-color:        #{$dark-background-color)};
    --light-bg-color:       #{lighten($dark-background-color, 5%))};
    --dark-bg-color:        #{darken($dark-background-color, 5%))};

    --base-text-color:      #{$dark-text-color)};
    --fade-text-color:      #{darken($dark-text-color, 25%))};
}
```

### The future's so bright, I gotta wear shades
![](/img/2021/omg-so-bright.png "web page with light color scheme"){:.right.max25}

Down, and down, we go.

With the theming rewrite, it's much easier to define variations of the theme, and let `@media`{:.nowrap} selectors do the work of picking the correct one. In the future this can easily be extended to also accomodate e.g. _high contrast_ preferences.

This is the first stab of the light color scheme, that will be presented to viewers with a preference of being blinded, but this will take more work to get right.

Code syntax higlighting blocks still use the dark theme, because code is supposed to be read in the darkness anyway.

{:.clear}
```scss
$light-gray-color:          $gray-color;
$light-background-color:    lighten($light-gray-color, 40%);
$light-text-color:          darken($light-gray-color, 45%);

@media screen and (prefers-color-scheme: light) {
    :root {
        --base-bg-color:    #{$light-background-color)};
        --light-bg-color:   #{lighten($light-background-color, 5%))};
        --dark-bg-color:    #{darken($light-background-color, 5%))};

        --base-text-color:  #{$light-text-color)};
        --fade-text-color:  #{lighten($light-text-color, 25%))};
    }
}
```
