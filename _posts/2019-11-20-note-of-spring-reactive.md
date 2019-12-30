---
title: "Notes of Spring Reactive"
layout: single
cover: false
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'posts'
comments: true
date: 2019-11-20 09:36:43 EST
---

## Reactive programming

- [](https://github.com/hantsy/spring-reactive-sample)

## Spring WebFlux

- [Spring WebFlux](https://docs.spring.io/spring/docs/current/spring-framework-reference/web-reactive.html)
- [Passing context with spring WebFlux](https://ndportmann.com/passing-context-with-spring-webflux/)
- [Doing stuff with Spring WebFlux](https://lankydan.dev/2018/03/15/doing-stuff-with-spring-webflux)
- [Authentication and Authorization Using JWT on Spring Webflux](https://medium.com/@ard333/authentication-and-authorization-using-jwt-on-spring-webflux-29b81f813e78)

## Passing context between steps in the pipeline

- [Contextual Logging with Reactor Context and MDC](https://simonbasle.github.io/2018/02/contextual-logging-with-reactor-context-and-mdc/)

## Reactive Spring Data

- [Srping Data Cassandra Reactive](https://www.baeldung.com/spring-data-cassandra-reactive)

## Handling errors

- [Handling Errors in Spring WebFlux](https://www.baeldung.com/spring-webflux-errors)
- [Reactor – Handle Error](https://grokonez.com/reactive-programming/reactor/reactor-handle-error#21_By_falling_back_to_another_Flux)


- switchIfEmpty

```java
        return Mono
                .just(
                        repository.findById(id)
                )
                .switchIfEmpty(Mono.error(new HttpClientErrorException(HttpStatus.BAD_REQUEST, "")))
                .flatMap(entity -> repository.updateById(id, entity))
                .map(createdEntity -> conversionService.convert(createdEntity, TargetObject.class));
        // @formatter:on
```

## Spring Reactive WebClient


### Create WebClient with custom connect/read [[timeout]]
```java
private WebClient createWebClientWithConnectAndReadTimeOuts(int connectTimeOut, long readTimeOut) {
        // create reactor netty HTTP client
        HttpClient httpClient = HttpClient.create()
                .tcpConfiguration(tcpClient -> {
                    tcpClient = tcpClient.option(ChannelOption.CONNECT_TIMEOUT_MILLIS, connectTimeOut);
                    tcpClient = tcpClient.doOnConnected(conn -> conn
                            .addHandlerLast(new ReadTimeoutHandler(readTimeOut, TimeUnit.MILLISECONDS)));
                    return tcpClient;
                });
        // create a client http connector using above http client
        ClientHttpConnector connector = new ReactorClientHttpConnector(httpClient);
        // use this configured http connector to build the web client
        return WebClient.builder().clientConnector(connector).build();
    }
```


## Sample projects

- [BUILD REST API WITH REACTIVE SPRING](https://iseif.dev/2019/04/12/rest-api-with-reactive-spring/)
- [Tuto - Building a Reactive RESTful API with Spring WebFlux Java](https://medium.com/@cheron.antoine/tuto-building-a-reactive-restful-api-with-spring-webflux-java-258fd4dbae41)
- [Authentication and Authorization Using JWT on Spring Webflux](https://medium.com/@ard333/authentication-and-authorization-using-jwt-on-spring-webflux-29b81f813e78)
