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

```bash
qaq " what this does is to clear the content of the register 'a'
:g/pattern/y A " what this does is to copy the search result to register 'a'
:tabnew "create a new tab
"ap "paste the content of register 'a' to the current buffer
```

##### Related reference
- [power of g](http://vim.wikia.com/wiki/VimTip227)

### Append characters at the end of lines

```bash
# assume you just want to append a ',' at the end of each line
:%s /$/,/
```

### Surround each line with double quotes

```bash
:%s /.*/"&"/
```

### Swap matched gruops

e.g. you have a string like `a -> b`, and want to swap it to `b -> a`

What you need to do is:

```bash
:%s /\(\w*\) -> \(\w*\)/\2 -> \1/g
```

> Note: what's tricky here is that you have to escape '(,)' using '\'

### YouCompleteMe
[YouCompleteMe](https://valloric.github.io/YouCompleteMe/) is a fantastic vim plugin that help you write code more easily.

Here is the command I typically use to build the library:

```bash
cd ~/.vim/plugged/YouCompleteMe
./install.sh --tern-completer
```

### Spell check

```bash
:set spell
:set spell spelllang=en
:set nospell
]s move to next error
[s move to previous error
z= suggest a list of alternatives
zg add the current word to dictionary
zug cancel dictionary update
```

### CtrlP commands

Change the root folder used by `CtrlP`:

```bash
CtrlPDir=~/abc
```

### MacVim settings

There are some special(`weird`) settings about `MacVim`, which has made me so confused. e.g. to set the `font` size or `colorscheme`, the settings you have in `.vimrc` don't work as you expect. The reality is that you have to configure those in `.gvimrc` instead of `.vimrc`. Take a look at this [.gvimrc](https://github.com/mingliangguo/mydotfiles/blob/master/.gvimrc) for what the settings look like.

