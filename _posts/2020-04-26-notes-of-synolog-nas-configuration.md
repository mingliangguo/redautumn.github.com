---
title: "Notes of Synolog NAS configuration"
layout: single
cover: false
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'posts'
comments: true
category: blog
date: 2020-04-26 13:12:09 EDT
---


## Setup Git Server

It's easy to install the git server using package center. What could be tricky is to setup the user access:

- create a user named as `git` from control panel.
- grant git access in the git server (by opening the git server from installed packages in package center)
- also make sure a user folder is created for the `git` user, which can be done in `Control Panel` -> `Users` -> `Advanced` -> `Enable user home service`
- ssh to the synology server and create a `git-shell-commands` folder under  `~git`, e.g. `mkdir ~git/git-shell-commands`
- If a custom ssh port is used, you need to use the following git command to specify the ssh port:
  - `git clone ssh://git@mydomain.com:[port]/gitrepo`
