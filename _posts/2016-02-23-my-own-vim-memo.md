---
title: "my own vim memo"
layout: post
cover: false
categories: 'blog'
tags: 'blog vim'
navigation: True
subclass: 'post tag-speeches'
comments: true
logo: 'assets/images/ghost.png'
cover: 'assets/images/cover4.jpg'
date: 2016-02-23 20:02:10 EST
---

This post just tries to summarize some frequently used vim commands that I can not remember (which is unforuante):

### Copy matched search result to a different buffer

```
qaq " what this does is to clear the content of the register 'a'
:g/pattern/y A " what this does is to copy the search result to register 'a'
:tabnew "create a new tab
"ap "paste the content of register 'a' to the current buffer
```

##### Related reference
- [power of g](http://vim.wikia.com/wiki/VimTip227)


