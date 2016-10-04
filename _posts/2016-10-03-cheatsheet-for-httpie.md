---
title: "Cheatsheet for Httpie"
layout: post
cover: false
categories: 'blog programmer web'
tags: 'blog web http'
navigation: True
subclass: 'post tag-speeches'
comments: true
logo: 'assets/images/ghost.png'
cover: 'assets/images/cover4.jpg'
date: 2016-10-03 12:49:27 EDT
---

[Httpie](https://httpie.org/) is a fantastic command line tool that help you do more http interations using the command prompt, similar to curl, but much much better.

## Make http GET with authorization header
```
http -v https://api.box.com/2.0/files/12345678 'Authorization:Bearer <access_token>'
```
