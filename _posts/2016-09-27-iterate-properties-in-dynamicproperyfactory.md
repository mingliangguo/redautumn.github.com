---
title: "Iterate properties in DynamicProperyFactory"
layout: post
cover: false
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'post tag-speeches'
comments: true
logo: 'assets/images/ghost.png'
cover: 'assets/images/cover4.jpg'
date: 2016-09-27 20:16:06 EDT
---

This might not be a common scenario, but sometimes you might need to iterate all of the properties managed by [archaius](https://github.com/Netflix/archaius) utlity. Here is the code that can you do it:

```java
Object config = DynamicPropertyFactory.getBackingConfigurationSource();
if (DynamicPropertyFactory.isInitializedWithDefaultConfig()) {
    ConcurrentCompositeConfiguration composite = (ConcurrentCompositeConfiguration) config;
    Properties p = composite.getProperties();

    Iterator<Object> it = p.keySet().iterator();
    while (it.hasNext()) {
        String name = (String) it.next();
        DynamicStringProperty value = DynamicPropertyFactory.getInstance().getStringProperty(name, null);
    }
}
```


