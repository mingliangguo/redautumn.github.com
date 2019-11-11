---
title: "Debug java application"
layout: single
cover: false
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'posts'
comments: true
date: 2019-11-03 20:48:52 EST
---

Just use this post to write down some techniques about debugging java applications, especially for multi-thread, deadlock or memory issues.

For IBM JDK, use the following command to trigger thread dump.

```bash
kill -3 pid
```

For Open JDK

```bash
jps
jstack
```
