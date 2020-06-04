---
title: "Notes of hystrix configuration"
layout: single
cover: false
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'posts'
comments: true
category: blog
date: 2020-05-14 11:14:10 EDT
---

## Hystrix configuration

Everything you need to know about the hystrix configuration:

- [Hystrix Configuration](https://github.com/Netflix/Hystrix/wiki/Configuration)

## A standard hystrix configuration to start with


```yaml
hystrix:
  circuitBreaker:
    enabled: ${HYSTRIX_CIRCUITBREAKER_ENABLED:true}
    requestVolumeThreshold: ${HYSTRIX_CIRCUITBREAKER_REQUEST_VOLUME_THRESHOLD:20}
    sleepWindowInMilliseconds: ${HYSTRIX_CIRCUITBREAKER_SLEEP_WINDOW_IN_MILLIS:5000}
    errorThresholdPercentage: ${HYSTRIX_CIRCUITBREAKER_ERROR_THRESHOLD_PERCENTAGE:50}
  collapser:
    default:
      maxRequestsInBatch: 50
  threadpool:
    default:
      coreSize: ${HYSTRIX_THREAD_POOL_CORE_SIZE:200}
      maxQueueSiz: ${HYSTRIX_THREAD_POOL_MAX_QUEUE_SIZE:-1}
      maximumSize: ${HYSTRIX_THREAD_POOL_MAX_SIZE:400}
      allowMaximumSizeToDivergeFromCoreSize:  ${HYSTRIX_THREAD_POOL_ALL_DIVERGE:true}
  command:
    default:
      execution:
        isolation:
          strategy: ${HYSTRIX_DEFAULT_EXECUTION_ISOLATION_STRATEGY:THREAD}
          semaphore:
            maxConcurrentRequests: 5000
          timeout:
            enabled: ${HYSTRIX_DEFAULT_EXECUTION_TIMEOUT_ENABLED:true}
          thread:
            interruptOnTimeout: ${HYSTRIX_DEFAULT_EXECUTION_INTERRUPT_ON_TIMEOUT:true}
            timeoutInMilliseconds:  ${HYSTRIX_DEFAULT_EXECUTION_TIMEOUT_IN_MILLIS:4000}
```

## Enable Hystrix dashboard for troubleshooting

### Dependencies to add for spring-boot applications:

```
  implementation platform("org.springframework.boot:spring-boot-dependencies:$SPRING_BOOT_VERSION")
  implementation "org.springframework.boot:spring-boot-starter"
  implementation "org.springframework.boot:spring-boot-starter-actuator"

  implementation  platform("org.springframework.cloud:spring-cloud-dependencies:${SPRING_CLOUD_BOM_VERSION}")
  implementation "org.springframework.cloud:spring-cloud-starter"
  implementation "org.springframework.cloud:spring-cloud-starter-netflix-hystrix"
  implementation "org.springframework.cloud:spring-cloud-starter-netflix-hystrix-dashboard"
  implementation "org.springframework.cloud:spring-cloud-starter-netflix-archaius"

```

### Configurations to enable hystrix dashboard

```yaml
management:
  endpoint:
    health:
      enabled: true
      show-details: ALWAYS
  endpoints:
    jmx:
      exposure:
        include: "*"
    web:
      base-path: '/actuator'
      exposure:
        include: "*"
```

## Code analysis

- [Talk about the execution.isolation.semaphore.maxconcurrentquests property of hystrix](https://ddcode.net/2019/06/21/talk-about-the-execution-isolation-semaphore-maxconcurrentquests-property-of-hystrix/)
