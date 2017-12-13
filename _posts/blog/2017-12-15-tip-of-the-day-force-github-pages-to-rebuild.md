---
author: juanpintoduran
title: '[Daily Tip] How to force GitHub pages to rebuild'
excerpt:
layout: post
category:
  - Tips
tags:
  - development
post_format: [ ]
---

This is both a `git` tip for some, but the only real usage that I have for this command is to force GitHub pages to rebuild this blog without making any changes to it:

```
git commit -m 'REBUILD ALL THE THINGS!' --allow-empty
git push origin master
```
