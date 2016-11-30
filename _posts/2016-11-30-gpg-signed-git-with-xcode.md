---
layout: post
title: GPG signed Git with XCode
category: devlog
tags:
- xcode
---
For [work projects](https://github.com/saab-simc-admin/) I've been working on lately, we have adopted a strict gpg signed commits and tags only policy, so I thought I'd carry that good intention over to private projects as well. Except it turns out that the execution environment in which XCode runs git does not play well with gnupg.

```
gpg: cannot open `/dev/tty': Device not configured
```

Searching for solutions got me nothing but "not supported". So sad. Can't be.

{%gist notCalle/da9c3c4e6c82381835059dea2422b645 %}
```sh
% git config --global gpg.program gpg-batch
```

Ta-da! You're welcome.
