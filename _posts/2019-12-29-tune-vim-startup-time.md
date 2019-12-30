---
title: "Tune vim startup time"
layout: single
cover: false
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'posts'
comments: true
date: 2019-12-29 23:06:12 EST
---

My vim has been quite slow on startup and I really want to make it faster, otherwise it would be a pain to use vim, which should not be the case!

There are multiple ways to profile the startup time of vim:
- The native profiler vim provides, see this [stackoverflow question](https://stackoverflow.com/questions/12213597/how-to-see-which-plugins-are-making-vim-slow)
- [vim-startuptime-benchmark](https://github.com/junegunn/vim-startuptime-benchmark)
- [vim-plugins-profile](https://github.com/hyiltiz/vim-plugins-profile)

The tool I chose to use is: [vim-plugins-profile](https://github.com/hyiltiz/vim-plugins-profile), which I found is much easier to use. It provides scripts in different languages for use. The bash script seems requiring the `R` to be installed. The one I chose to use is the python script, which is really use to use. Since I use [neovim](https://neovim.io/), here is the command I use:

```bash
python vim-plugins-profile.py nvim
```

The scripts gives you the top ten most time-consuming plugins. And that's what you should look into to improve the startup time. For me, the following plugins took long time to load:

- [vimwiki](https://github.com/vimwiki/vimwiki)
- [vim-prettier](https://github.com/prettier/vim-prettier)

Since I don't use them on all scenarios, the strategy I use is to lazy load them, i.e. only load them when needed. Fortunately the plugin manager [vim-plug](https://github.com/junegunn/vim-plug) has already provided the `on-demand loading` mechanism for this. Checkout the *Plug* options for the on-demand loading. There are two different options:
- `on` on	On-demand loading: Commands or `<Plug>`-mappings
- `for`	On-demand loading: File types

Since `vim-prettier` is primarily for front-end development and its author actually provides an example of how to lazy load the plugin, which is exactly what I need (not sure why I didn't use it at the beginning.):

```bash
Plug 'prettier/vim-prettier', {
  \ 'do': 'yarn install',
  \ 'for': ['javascript', 'typescript', 'css', 'less', 'scss', 'json', 'graphql', 'markdown', 'vue', 'yaml', 'html'] }
```

For `vim-wiki`, as it's only used for editing my personal wiki, I don't need it to be loaded all the time. To lazy load it, there are two different options:

- to enable it for some particular file types - `for`, which is how it's done for `vim-prettier`.
- to enable it for some particular command, which is the `on` command in `vim-plug`

As I don't need to enable `vimwiki` most of the time, I decided to load it via a command. i.e. to enable it, `:VimwikiUISelect` has to be typed.

Using this technique, I also converted couple of the other slow plugins to be loaded on-demand. After doing these, now my vim starts super-fast! And I am very happy with the result!
