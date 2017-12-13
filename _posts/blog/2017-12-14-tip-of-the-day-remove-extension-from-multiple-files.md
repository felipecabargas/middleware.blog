---
author: juanpintoduran
title: '[Daily Tip] How to remove the extension of multiple files at once (CLI)'
excerpt:
layout: post
category:
  - Tips
tags:
  - development
post_format: [ ]
---

This is another simple one (tested on both Linux & Mac):

```
find ./ -name '*.ext' | while read f; do mv "$f" "${f%.ext}"; done
```

Change `ext` for your desired extension.

Using `find` is better than using `replace` because the latter will replace the first match of `.ext` instead.
