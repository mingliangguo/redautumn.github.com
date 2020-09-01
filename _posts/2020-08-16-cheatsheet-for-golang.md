---
title: "Cheatsheet for golang"
layout: single
cover: false
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'posts'
comments: true
category: blog
date: 2020-08-16 13:51:48 EDT
---

## Run tests

```bash
go test ./... # run all tests in current directory and all of its sub-directories
go test ./a/... ./b/... # run tests for some particular directories
go test ... # run all tests in your $GOPATH
```

## Specify default values for json parsing

- https://stackoverflow.com/questions/30445479/how-to-specify-default-values-when-parsing-json-in-go


## Tools

- [An Overview of Go's Tooling](https://www.alexedwards.net/blog/an-overview-of-go-tooling)
