---
title: "switch from vundle to vim-plug for vim plugin manager"
layout: post
cover: false
categories: 'blog'
tags: 'blog'
navigation: True
fullview: true
comments: true
subclass: 'post tag-speeches'
logo: 'assets/images/ghost.png'
cover: 'assets/images/cover4.jpg'
date: 2016-01-25 13:56:21 EST
---

I have been using [vundle](https://github.com/VundleVim/Vundle.vim) to manage my vim plugins for quite a while. It works pretty well. However, I just found a new option very recently - [vim-plug](https://github.com/junegunn/vim-plug). vim-plug does provide a lot more options to manage your vim plugins, e.g. it supports defining post actions for each of plugin. This could be very helpful for plugins that need to compile or install. Some good examples are:

```
" Plugin outside ~/.vim/plugged with post-update hook
Plug 'junegunn/fzf', { 'dir': '~/.fzf', 'do': './install --all' }
```

One article which led me to vim-plug is - [Why I switched from Vundle to Plug](https://jordaneldredge.com/blog/why-i-switched-from-vundle-to-plug/). Thanks for the tip!

And this article [How to Switch from Vundle to vim-plug](http://www.adamwadeharris.com/how-to-switch-from-vundle-to-vim-plug/) also contains very helpful information about how to switch from vundle to vim-plug. But minimally, if you just want to switch, you can pretty much replace Plugin to Plug in your .vimrc file and also make sure change the vundle#begin()/vundle#end()  to plug#bengin()/plug#end(), as following:

```
call plug#begin('~/.vim/plugged')

" Plugins go here

call plug#end()
```
