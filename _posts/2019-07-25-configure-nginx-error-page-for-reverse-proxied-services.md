---
title: "configure nginx error page for reverse proxied services"
layout: single
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'post tag-speeches'
comments: true
date: 2019-07-25 14:46:19 EDT
---

The basic idea is to use nginx for

- turn on `proxy_intercept_errors on;` in the downstream service configuration.
- define the error page at the upper level server configuration.

Refer to this article:

- https://erikzaadi.com/2014/06/23/handle-proxy-404-in-nginx/
- https://guides.wp-bullet.com/nginx-redirect-404-errors-to-homepage-wordpress/
