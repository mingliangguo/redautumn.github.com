---
title: "my git cheatsheet"
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
date: 2016-02-04 13:21:56 EST
---

Just to keep a note about some frequently used git commands:

#### Push an existing project to a remote repository

```
# in your remote repo
git init --bare my-project.git

# in your local project folder
git init
git add .
git commit -m 'initial commit'
git remote add origin git@your-git-host:gitRepot/my-project.git
git push origin master
```


