---
title: "Rest client logging in spring boot"
layout: single
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'post tag-speeches'
comments: true
date: 2019-07-23 11:04:44 EDT
---


## Feign client


https://cloud.spring.io/spring-cloud-netflix/multi/multi_spring-cloud-feign.html

> A logger is created for each Feign client created. By default the name of the logger is the full class name of the interface used to create the Feign client. Feign logging only responds to the DEBUG level.

> application.yml.

> logging.level.project.user.UserClient: DEBUG
The Logger.Level object that you may configure per client, tells Feign how much to log. Choices are:

> NONE, No logging (DEFAULT).
> - BASIC, Log only the request method and URL and the response status code and execution time.
> - HEADERS, Log the basic information along with request and response headers.
> - FULL, Log the headers, body, and metadata for both requests and responses.
> For example, the following would set the Logger.Level to FULL:

```java
@Configuration
public class FooConfiguration {
    @Bean
    Logger.Level feignLoggerLevel() {
        return Logger.Level.FULL;
    }
}
```


Question: Need to understand if this configuration works with log4j2 configuration.


## REST Template

https://blog.morizyun.com/java/spring-resttemplate-debug-logging.html

### Best for debugging (header wire + context logging)

```
log4j.logger.httpclient.wire.header=DEBUG
log4j.logger.org.apache.commons.httpclient=DEBUG

```

### Enable full wire (header and content) + context logging

```
log4j.logger.httpclient.wire=DEBUG
log4j.logger.org.apache.commons.httpclient=DEBUG

```
## HttpClient


http://hc.apache.org/httpclient-3.x/logging.html
