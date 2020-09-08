---
title: "Setup Gitbook on MacOS"
layout: single
cover: false
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'posts'
comments: true
category: blog
date: 2020-09-07 13:52:23 EDT
---

## Install gitbook CLI

Somehow the [gitbook-cli](https://github.com/GitbookIO/gitbook-cli) doesn't support the latest [npm](https://www.npmjs.com). To properly install [gitbook-cli](https://github.com/GitbookIO/gitbook-cli), follow the steps below:

1. Install [nvm](https://github.com/nvm-sh/nvm)
2. Use `nvm install 9`, which gives `npm` version `5.60`
3. Install `gitbook-cli` using: `npm install -g gitbook-cli`
4. Start enjoying `gitbook` CLI.
  - `gitbook install`
  - `gitbook build`
  - `gitbook serve`



## Use Gitbook

Follow this [Content Configuration](https://docs.gitbook.com/integrations/github/content-configuration) to configure a githook repository.


## References

- [How to build gitbook with gitbook-cli](https://github.com/chusiang/how-to-build-the-gitbook-with-gitbook-cli)
