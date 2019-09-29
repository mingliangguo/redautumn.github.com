---
title: "Connect to mysql in MAMP from terminal in Mac"
layout: single
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'post tag-speeches'
comments: true
date: 2016-08-15 23:07:33 EDT
---

If you use MAMP and want to connect mysql from terminal, you should use the following command:

1. Launch MAMP
2. Start MySql server or all servers
3. Launch terminal/iterm2, type the command as following:

```bash
$ cd /Applications/MAMP/Library/bin
$ ./mysql --host=localhost -uroot -proot
```
