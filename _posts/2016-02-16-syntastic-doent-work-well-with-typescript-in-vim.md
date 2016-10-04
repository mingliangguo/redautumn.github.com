---
title: "Syntastic doen't work well with typescript in vim"
layout: post
cover: false
categories: 'blog'
tags: 'blog vim typescript'
navigation: True
comments: true
subclass: 'post tag-speeches'
logo: 'assets/images/ghost.png'
cover: 'assets/images/cover4.jpg'
date: 2016-02-16 20:45:38 EST
---

I ran into some issues with syntax checking for typescript code in vim. I have been using [Syntastic](https://github.com/scrooloose/syntastic) for quite a while, and it has been very helpful for all the other languages I work with. But this time, it seems that I have run into a bug or issue with it.

Basically the issue is it can not properly support the different target for a typescript code. Typescript uses a tsconfig.json to store the compilation target information and many other options. However, Syntastic doesn't honor these configuration. And it will display some compilation errors, which is quite annoying.

By a little bit searching, I found I am not alone, here is a similar issue reported in [github](https://github.com/leafgarland/typescript-vim/issues/47).

Inspired by this post, what I did is to add the following line in my .vimrc:

```bash
let g:syntastic_typescript_tsc_args = "-t ES5 -m commonjs --experimentalDecorators --emitDecoratorMetadata --sourceMap true --moduleResolution node"
```

Aparently, this is not ideal! What if I have projects with different targets or configurations. It would be ideal if these plugins could use the settings in tsconfig.json. Before that, I might consider to use [vscode](https://code.visualstudio.com/) for typescript code.

The following is the link you can find the compiler options for typescript:

- [Type script compiler options](https://github.com/Microsoft/TypeScript/wiki/Compiler-Options)

