---
title: "mingliang.me is the domain name now"
layout: post
cover: false
categories: 'blog'
tags: 'blog'
fullview: true
comments: true
navigation: True
subclass: 'post tag-speeches'
logo: 'assets/images/ghost.png'
cover: 'assets/images/cover4.jpg'
date: 2016-02-11 11:49:07 EST
---

In fact, I have used this domain name a while back. And I just decided to pick it up again. To use a custom domain name with github pages is fairly simple. What you need to do is:

- Create a CNAME file in your github pages repo, which points to your custom domain name (i.e. mingliang.me)
- Create CNAME records in your DNS manager (e.g. GoDaddy, Name.com, NameCheap, etc.) 
  - One for the root apex (@) and one for www. Both point to yourusername.github.io. 
  - If your DNS provider does NOT support ALIAS records on the root apex (@), simply create A records that point to 192.30.252.153 and 192.30.252.154

That's it!!

Here are some links if you still don't get it:

- [Adding a CNAME file to your repository](https://help.github.com/articles/adding-a-cname-file-to-your-repository/)
- [Setting the DNS for GitHub Pages on Namecheap](http://www.hongkiat.com/blog/github-with-custom-domain/)
