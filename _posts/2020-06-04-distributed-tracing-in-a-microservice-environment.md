---
title: "Distributed tracing in a microservice environment"
layout: single
cover: false
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'posts'
comments: true
category: blog
date: 2020-06-04 11:34:44 EDT
---

Feign Rest Client
https://cloud.spring.io/spring-cloud-sleuth/reference/html/#feign

By default, Spring Cloud Sleuth provides integration with Feign through TraceFeignClientAutoConfiguration. You can disable it entirely by setting spring.sleuth.feign.enabled to false. If you do so, no Feign-related instrumentation take place.

Part of Feign instrumentation is done through a FeignBeanPostProcessor. You can disable it by setting spring.sleuth.feign.processor.enabled to false. If you set it to false, Spring Cloud Sleuth does not instrument any of your custom Feign components. However, all the default instrumentation is still there.

References

## Distributed tracing support in NewRelic

- [Getting Started With New Relic Distributed Tracing](https://blog.newrelic.com/product-news/distributed-tracing-general-availability/)
NR supports auto instrument, which looks pretty cool. And not sure how well it works with the infinite tracing feature. If it could provides tracing for all requests, it would be awesome. And there are no needs to setup spring sleuth or zipkin if NR is used.
NR supports both infinite tracing and head based tracing.

- [Infinite tracing v.s. head tracing](https://docs.newrelic.com/docs/understand-dependencies/distributed-tracing/infinite-tracing/introduction-infinite-tracing)

## References

- https://istio.io/faq/distributed-tracing/
- https://blog.newrelic.com/engineering/opentelemetry-opentracing-opencensus/
- https://blog.newrelic.com/product-news/distributed-tracing-general-availability/
- https://docs.newrelic.com/docs/understand-dependencies/distributed-tracing/get-started/how-new-relic-distributed-tracing-works
- [Microservices Distributed Tracing with Node.js and OpenTracing \| @RisingStack](https://blog.risingstack.com/distributed-tracing-opentracing-node-js/)
- [Adding tracing with Jaeger to an express application](https://rhonabwy.com/2019/01/06/adding-tracing-with-jaeger-to-an-express-application/)
