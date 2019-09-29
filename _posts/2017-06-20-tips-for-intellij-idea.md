---
title: "Tips for Intellij Idea"
layout: single
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'post tag-speeches'
comments: true
date: 2017-06-20 10:40:12 EDT
---


If you want to launch a project from command line, you can use the command line tool to do it. The cli tool doesn't install with Intellij, you have to install it separately from `Tools -> Install command line launcher`. By default, the launcher will be installed into `/usr/local/bin/idea`, so you don't have to add it to the path.

Once it's installed, you can go to terminal and use it to launch Intellij, e.g.

```bash
idea .
idea pom.xml
idea build.gradle
```


