---
title: "enable disqus comment for jekyll website"
layout: post
cover: false
categories: 'blog'
tags: 'blog jekyll'
navigation: True
subclass: 'post tag-speeches'

comments: true
logo: 'assets/images/ghost.png'
cover: 'assets/images/cover4.jpg'
date: 2016-02-20 21:39:36 EST
---

It is fairly simple to enable [disqus](https://disqus.com) for jekyll. 

- First you need to register an account in disqus, then you need to setup disqus for your webiste in disqus' web [admin ui](https://disqus.com/admin/create/)
- From the setup admin ui, you will be asked to choose a unique disqus URL for your website. This is the URL will be embedded to your website for commeting. So pleae remember this URL.
- Add the short unique name in your disqus URL to your jekyll _config.yml file. For example, if your disqus URL is mycoolblog.disqus.com, then mycoolblog is the id you need to configure in jekyll.

```
disqus: mycoolblog
```

### Note:

Disqus comment is not enabled by default in jekyll. To enable it, add comments=true in your post header.

```
comments: true
```





