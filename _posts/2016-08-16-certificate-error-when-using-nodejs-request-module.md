---
title: "Certificate error when using nodejs request module"
layout: single
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'post tag-speeches'
comments: true
date: 2016-08-16 23:13:54 EDT
---

I created a nodejs client to test our application. The application is still using a self-signed certificate to run https. So I got this error when I try to call the services using request API..

```bash
{ [Error: self signed certificate] code: 'DEPTH_ZERO_SELF_SIGNED_CERT' }
```

By some searching, the easiest way to fix it or workaround seems to set the following flag to ignore it, and it works well!

```bash
process.env.NODE_TLS_REJECT_UNAUTHORIZED = "0"
```
