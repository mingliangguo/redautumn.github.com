---
title: "Github workflows"
layout: single
cover: false
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'posts'
comments: true
date: 2019-10-31 20:26:28 EDT
---

Use this post to summarize some workflows I uses in my daily development.


## Using [hub](https://github.com/github/hub) with enterprise Github


### Configuration

My company uses enterprise github for source code management. To use `hub` with enterprise github, what you need to do is basically just two things:

- `git config --global --add hub.host YOUR_ENTERPRISE_GIHUB_DOMAIN`
- `export GITHUB_TOKEN=your_token`

That's all you need for configuration.

### Hub usage

##### Create pull request

```bash
hub pull-request --base your_org:your_master-branch
hub pull-request --no-edit -F ~/temp/pr_summary.md
```
