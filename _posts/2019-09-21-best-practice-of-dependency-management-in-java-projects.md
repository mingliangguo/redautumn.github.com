---
title: "Best practice of dependency management in Java projects"
layout: post
cover: false
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'post tag-speeches'
comments: true
logo: 'assets/images/ghost.png'
cover: 'assets/images/cover4.jpg'
date: 2019-09-21 12:13:46 EDT
---

It is pretty common for a modern java project to use `Maven` or `Gradle` to help manage the dependencies, which usually works pretty well for small project or single project. (If you are still managing the dependencies manually, you should definitely start using either of which!!) However when you are working in a much complex project which involves many projects depends on each other, which is actually pretty common in a micro-service world.

Here are some best practices that will help you make the dependency management easier:

- Get a good understanding of the scopes used for the dependencies in `Gradle` or `Maven`
- Usee `BOM` whenever possible to help you manage the specific version of dependencies.
  - Avoid adding any dependencies explicitly if possible
