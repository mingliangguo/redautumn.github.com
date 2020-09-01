---
title: "Fluentd log collector in kubernetes"
layout: single
cover: false
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'posts'
comments: true
category: blog
date: 2020-08-01 13:02:21 EDT
---


## Kubernetes logging architecture

- https://kubernetes.io/docs/concepts/cluster-administration/logging/#cluster-level-logging-architectures


## Graylog

- https://docs.graylog.org/en/3.2/pages/gelf.html#sending-gelf-messages-via-http-using-curl

```bash
# send log message via GELF UDP
echo -n '{ "version": "1.1", "host": "example.org", "short_message": "A short message", "level": 5, "_some_info": "foo" }' | nc -w0 -u graylog.example.com 12201

# send log message via GELF TCP
echo -n -e '{ "version": "1.1", "host": "example.org", "short_message": "A short message", "level": 5, "_some_info": "foo" }'"\0" | nc -w0 graylog.example.com 12201

# send log message via GELF HTTP
curl -X POST -H 'Content-Type: application/json' -d '{ "version": "1.1", "host": "example.org", "short_message": "A short message", "level": 5, "_some_info": "foo" }' 'http://graylog.example.com:12201/gelf'
```

- Configure graylog to work with fluentd: https://docs.fluentd.org/how-to-guides/graylog2
- Be aware of the payload schema of the Gelf payload, which only supports a few known properties, and for the other unknown ones, the property name has to be prefixed with `_`. https://docs.graylog.org/en/3.2/pages/gelf.html

## Fluentd

- [Fluentd v.s. Fluentd Bit](https://fluentbit.io/documentation/0.8/about/fluentd_and_fluentbit.html)
  - > As described in the table, if the target environment is a server with common capacity, Fluentd is a great option due to it flexibility and availability of plugins (more than 300 extensions!) but if the data collection will happen in an Embedded environment or an IoT device where the system capacity is restricted, Fluent Bit is the solution to use.
- [Fluentd regular expression app](https://fluentular.herokuapp.com/)

## References

- https://medium.com/kubernetes-tutorials/cluster-level-logging-in-kubernetes-with-fluentd-e59aa2b6093a

