---
title: "unexpected token error with Angular2"
layout: post
cover: false
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'post tag-speeches'
comments: true
logo: 'assets/images/ghost.png'
cover: 'assets/images/cover4.jpg'
date: 2016-03-02 23:43:41 EST
---
I was playing with [Angular2](https://angular.io/) recently and it has been a quite enjoyful expeirence, until I ran into the 'unexpected token <' error:

```
uncaught SyntaxError: Unexpected token < - http:1
uncaught SyntaxError: Unexpected token < - angular2-polyfills.js:138
    evaluating http://localhost:3000/angular2/http
    error loading http://localhost:3000/app/boot.js
```

I spend some time to looking into the issue, and noticed that the response of http://localhost:3000/angular2/http is actually a html, not the right js file. I ran some search in Google and find that I am not alone. There are quite some questions in Stackoverflow for the same problem:

- [Angular2 beta - bootstrapping HTTP_PROVIDERS - “Unexpected Token <”](http://stackoverflow.com/questions/34401354/angular2-beta-bootstrapping-http-providers-unexpected-token/34402203#34402203)

Basically this is a problem about missing libraries. Some modules have to be added into html explicitly. I hope there is an easier way to figure out what need to be added when a class is used. 

The following is the fix if you run into the same http issue:

```
# if npm is used
<script src="node_modules/angular2/bundles/http.dev.js"></script>
# if cdn is used
<script src="https://code.angularjs.org/2.0.0-beta.0/http.dev.js"></script>
```
