---
title: "Error Handling Behavior of WebSphere Liberty TAI"
layout: post
cover: false
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'post tag-speeches'
comments: true
logo: 'assets/images/ghost.png'
cover: 'assets/images/cover4.jpg'
date: 2016-06-30 11:29:53 EDT
---



This is a sample project to demonstrate the usage of [WebSphere Liberty Trust Association Interceptor (TAI)](https://www.ibm.com/support/knowledgecenter/en/SSEQTP_8.5.5/com.ibm.websphere.wlp.doc/ae/twlp_dev_custom_tai.html). TAI is used in one of our projects as the authentication mechanism. It intercepts all requests coming to the server and determines if it's from an authenticated user or not. If it's not(or session expired, etc.), it will prompt the user to authenticate.


- [IBM WebSphere Developer Technical Journal: Advanced authentication in WebSphere Application Server](http://www.ibm.com/developerworks/websphere/techjournal/0508_benantar/0508_benantar.html)
