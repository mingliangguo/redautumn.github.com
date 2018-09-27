---
title: "deprecation in graphql"
layout: post
cover: false
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'post tag-speeches'
comments: true
logo: 'assets/images/ghost.png'
cover: 'assets/images/cover4.jpg'
date: 2018-09-27 10:51:41 EDT
---

Record the ways of deprecation in GraphQL.

For [GraphQL-Java](https://github.com/graphql-java/graphql-java), you can use annotations from [GraphQL-java-annotations](https://libraries.io/github/graphql-java/graphql-java-annotations) to annotate the deprecated fields.

`@GraphQLDeprecate` and Java's `@Deprecated` can be used to specify a deprecated field.

**Note:** GraphQL doesn't support deprecation of fields in input types. See [github discussion here](https://github.com/facebook/graphql/issues/197)
