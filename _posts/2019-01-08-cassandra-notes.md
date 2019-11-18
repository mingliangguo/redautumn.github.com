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

## Data modeling

- [Basic Rules of Cassandra Data Modeling](https://www.datastax.com/blog/2015/02/basic-rules-cassandra-data-modeling)

## Limitations of Materialized View

- [Known limitations of materialized views](https://docs.datastax.com/en/cql/3.3/cql/cql_using/knownLimitationsMV.html)
- [Cassandra Materialized Views ready for Production?](https://techblog.fexcofts.com/2018/05/08/cassandra-materialized-views-ready-for-production/)
- [Materialized Views marked experimental](https://www.mail-archive.com/user@cassandra.apache.org/msg54073.html)

## Performances

- [Cassandra performance: the most comprehensive overview you’ll ever see](https://www.scnsoft.com/blog/cassandra-performance)
- [Materialized View Performance in Cassandra 3.x](https://www.datastax.com/dev/blog/materialized-view-performance-in-cassandra-3-x)
- [Avoid pitfalls in scaling your Cassandra cluster: lessons and remedies](https://medium.com/walmartlabs/avoid-pitfalls-in-scaling-your-cassandra-cluster-lessons-and-remedies-a71ca01f8c04)
- [7 mistakes when using Apache Cassandra](https://blog.softwaremill.com/7-mistakes-when-using-apache-cassandra-51d2cf6df519)

### How to partition the data

- [Synthetic Sharding with Cassandra. Or How To Deal With Large Partitions.](https://medium.com/@foundev/synthetic-sharding-in-cassandra-to-deal-with-large-partitions-2124b2fd788b)

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
