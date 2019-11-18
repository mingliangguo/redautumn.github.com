---
title: "Note of Spring Couchbase support"
layout: single
cover: false
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'posts'
comments: true
date: 2019-10-31 22:13:14 EDT
---

## DDL

### create idnex

```bash
# create index
CREATE PRIMARY INDEX `foobucket_idx` ON `foodbucket`
# run query
select * from `foobucket` where id='test-1'
```

*NOTE* the bucket name has to be surrounded with '``'


## References

- [Spring Data Couchbase – Pitfalls to Avoid](http://hecodes.com/2019/07/spring-data-couchbase-pitfalls-to-avoid/)
- [Start Couchbase Using Docker Compose](https://blog.couchbase.com/couchbase-using-docker-compose/)
- [spring-data-couchbase:3.2.1 reference](https://docs.spring.io/spring-data/couchbase/docs/3.2.1.RELEASE/reference/html/#reference)
- [Couchbase with Spring-Boot and Spring Data](https://blog.couchbase.com/couchbase-spring-boot-spring-data/)
