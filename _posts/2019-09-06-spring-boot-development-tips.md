---
title: "spring boot development tips"
layout: post
cover: false
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'post tag-speeches'
comments: true
logo: 'assets/images/ghost.png'
cover: 'assets/images/cover4.jpg'
date: 2019-09-06 09:28:27 EDT
---


## Common application properties

- [Common application properties](https://docs.spring.io/spring-boot/docs/current/reference/html/common-application-properties.html)

## configuration to disable hystrix

```groovy
spring.cloud.circuit.breaker.enabled=false
hystrix.command.default.circuitBreaker.enabled=false
```


