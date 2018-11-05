---
title: "Memos for Java Stream API"
layout: post
cover: false
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'post tag-speeches'
comments: true
logo: 'assets/images/ghost.png'
cover: 'assets/images/cover4.jpg'
date: 2018-11-04 15:47:41 EST
---

## Stream.generate

```java
Random random = new Random();
List<Integer> numbers = Stream
    .generate(() -> random.nextInt(100))
    .limit(5)
    .collect(Collectors.toList());
```


