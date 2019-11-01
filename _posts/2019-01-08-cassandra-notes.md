---
title: "Cassandra Notes"
layout: single
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'post tag-speeches'
comments: true
date: 2019-01-08 10:39:12 EST
---


## Limitations of Materialized View

- [Known limitations of materialized views](https://docs.datastax.com/en/cql/3.3/cql/cql_using/knownLimitationsMV.html)
- [Cassandra Materialized Views ready for Production?](https://techblog.fexcofts.com/2018/05/08/cassandra-materialized-views-ready-for-production/)
- [Materialized Views marked experimental](https://www.mail-archive.com/user@cassandra.apache.org/msg54073.html)

## Performances

- [Cassandra performance: the most comprehensive overview you’ll ever see](https://www.scnsoft.com/blog/cassandra-performance)
- [Materialized View Performance in Cassandra 3.x](https://www.datastax.com/dev/blog/materialized-view-performance-in-cassandra-3-x)

## Pagination

- [Pagination support](https://docs.datastax.com/en/developer/java-driver/3.2/manual/paging/)

## Tombstones

- Partition tombstones
- Row tombstones
- Range tombstones
- ComplexColumn tombstones
- Cell tombstones
- TTL tombstones

Reference: [What are tombstones](https://docs.datastax.com/en/dse/5.1/dse-arch/datastax_enterprise/dbInternals/archTombstones.html)

Another very nice article describes issues around tombstones: https://thelastpickle.com/blog/2018/07/05/undetectable-tombstones-in-apache-cassandra.html


## Allow filtering

- [Allow filtering explained](https://www.datastax.com/blog/2014/12/allow-filtering-explained)

## In Query

Not using `in` query across multiple partitions, as explained in [this article](https://lostechies.com/ryansvihla/2014/09/22/cassandra-query-patterns-not-using-the-in-query-for-multiple-partitions/)
