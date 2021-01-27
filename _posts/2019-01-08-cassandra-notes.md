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

## When to use Cassandra

- [CASSANDRA USE CASES: WHEN TO USE AND WHEN NOT TO USE CASSANDRA](https://blog.pythian.com/cassandra-use-cases/)
- [When to use Cassandra and when to steer clear](https://towardsdatascience.com/when-to-use-cassandra-and-when-to-steer-clear-72b7f2cede76)

## Upgrade to cassandra 4.x driver and spring-data-cassandra 2.3.+

- [Upgrade to cassandra 4.x driver](https://docs.datastax.com/en/developer/java-driver/4.0/upgrade_guide/)
- [Spring Boot 2.3 Release Notes](https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-2.3-Release-Notes)

## CQL Tips

#### Using timestamp columns in cql where clause

Although Cassandra stores timestamp fractions using the `.ffffff` format defined by the ISO 8601 standard. However, when interacting with the database (ie. INSERT, SELECT, ...) you need to use the `.fff` format like so:

```bash
cqlsh:test_keyspace> select * from timestamp_table ;

timestamp                       | other_field
---------------------------------+---------------
2018-05-18 03:08:58.246000+0000 | Other content
2018-05-18 03:08:58.000000+0000 | Other content

cqlsh:test_keyspace> select * from timestamp_table WHERE timestamp='2018-05-18 03:08:58.123+0000';

timestamp                       | other_field
---------------------------------+---------------
2018-05-18 03:08:58.123000+0000 | Other content
```

## Data modeling

- [Basic Rules of Cassandra Data Modeling](https://www.datastax.com/blog/2015/02/basic-rules-cassandra-data-modeling)
- [CQL Limits](https://docs.datastax.com/en/cql/3.3/cql/cql_reference/refLimits.html)

## Limitations of Materialized View

- [Known limitations of materialized views](https://docs.datastax.com/en/cql/3.3/cql/cql_using/knownLimitationsMV.html)
- [Cassandra Materialized Views ready for Production?](https://techblog.fexcofts.com/2018/05/08/cassandra-materialized-views-ready-for-production/)
- [Materialized Views marked experimental](https://www.mail-archive.com/user@cassandra.apache.org/msg54073.html)
- [14 Things To Do When Setting Up a New Cassandra Cluster](https://thelastpickle.com/blog/2019/01/30/new-cluster-recommendations.html)
  - It's interesting that this article suggest disabling the materialized view when you setup a cassandra cluster. This might be a good advice!

## Performances

- [Cassandra performance: the most comprehensive overview you’ll ever see](https://www.scnsoft.com/blog/cassandra-performance)
- [Materialized View Performance in Cassandra 3.x](https://www.datastax.com/dev/blog/materialized-view-performance-in-cassandra-3-x)
- [Avoid pitfalls in scaling your Cassandra cluster: lessons and remedies](https://medium.com/walmartlabs/avoid-pitfalls-in-scaling-your-cassandra-cluster-lessons-and-remedies-a71ca01f8c04)
- [7 mistakes when using Apache Cassandra](https://blog.softwaremill.com/7-mistakes-when-using-apache-cassandra-51d2cf6df519)
- [Garbage Collection Tuning for Apache Cassandra](https://thelastpickle.com/blog/2018/04/11/gc-tuning.html)

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


## Batch

### `batch_size_warn_threshold_in_kb`
If you use `batch` with cassandra and saw warning in logs like this:
> BatchStatement.java:287 - Batch of prepared statements for [test, test1] is of size 6419, exceeding specified threshold of 5120 by 1299.

Normally this is not really harmful as it's just a warning. But you need to be careful about the usage of the `batch` and should avoid sending large paylaod to `batch` statement, especially when the statements are not against the same partition.


## Lightweight Transaction (LWT)

- [Cassandra Lightweight Transactions](https://www.beyondthelines.net/databases/cassandra-lightweight-transactions/)
- [DataStax - use LWT](https://docs.datastax.com/en/archived/cql/3.3/cql/cql_using/useInsertLWT.html)
