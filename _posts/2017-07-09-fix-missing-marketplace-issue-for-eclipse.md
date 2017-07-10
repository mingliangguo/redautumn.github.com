---
title: "Fix missing marketplace issue for eclipse"
layout: post
cover: false
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'post tag-speeches'
comments: true
logo: 'assets/images/ghost.png'
cover: 'assets/images/cover4.jpg'
date: 2017-07-09 23:05:16 EDT
---

I ran into a weird issue in eclipse, where the 'marketplace' menu is gone from the Help menu.

By some research, [this](https://bugs.eclipse.org/bugs/show_bug.cgi?id=518902) seems to be the way to resolve it.

- Open your `eclipse.ini` (The path is `/Applications/Eclipse\ JEE.app/Contents/Eclipse/` on mac)
- Add the following at the top:

>
```bash
-clean
-initialize
```

- Start your Eclipse once (it will stop on its own after a moment)
- Remove those entries again and restart Eclipse
- Check if the Marketplace entry is there now
