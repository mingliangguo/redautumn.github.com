---
title: "Redis Sentinel Note"
layout: single
cover: false
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'posts'
comments: true
category: blog
date: 2020-03-14 14:39:21 EDT
---

## Introduction

[Redis sentinel](https://redis.io/topics/sentinel) is the high availability solution offered by [Redis](https://redis.io/). In case of a failure in your Redis cluster, Sentinel will automatically detects the point of failure and bring the cluster back to stable mode without any human intervention. It will monitor your master & slave instances, notify you about changed behaviour, handle automatic failover in case a master is down and act as a configuration provider, so your clients can find the current master instance.

Redis Sentinel runs as a seperate program. You should have atleast 3 Sentinel instances monitoring a master instance and its slaves. Sentinel instances try to find consensus when doing a failover and only an odd number of instances will prevent most problems, 3 being the minimum. In this case one of the Sentinel instances can go down and a failover will still work as (hopefully) the other two instances reach consensus which slave to promote.

One thing about the configurable quorum: this is only the number of Sentinel who have to agree a master is down. You still need `N/2 + 1` Sentinels to vote for a slave to be promoted (that N is the total number of all Sentinels ever seen for this pod).

## How to check if the sentinel cluster works properly

1. connect to sentinel and find out the master nodes

```bash
# connect to sentinel server
redis-cli -h ${sentienal_host} -p ${sentinel_port}
# use the `info sentinel` command to get sentinel cluster info, you can find the master connection information in the sentinel section
info
# Sentinel
sentinel_masters:1
> sentinel_tilt:0
> sentinel_running_scripts:0
> sentinel_scripts_queue_length:0
> sentinel_simulate_failure_flags:0
> master0:name=mymaster,status=ok,address=172.20.0.3:6379,slaves=0,sentinels=1

# or you can use the sentinel command to get the master address
SENTINEL get-master-addr-by-name master-name ${master-name}
> localhost:26378> sentinel get-master-addr-by-name mymaster
> 1) "172.20.0.3"
> 2) "6379"
```

2. connect to the master node

```bash
# connect to redis master server
redis-cli -h ${master_host} -p ${master_port}

# once connected, you can use set/get to operate redis
> set foo "bar"
> get foo
```


## references

- [Redis Sentinel — High Availability: Everything you need to know from DEV to PROD: Complete Guide](https://medium.com/@amila922/redis-sentinel-high-availability-everything-you-need-to-know-from-dev-to-prod-complete-guide-deb198e70ea6)
- [Sentinel clients](https://redis.io/topics/sentinel-clients)
- [Reids Sentinel Cheat Sheet](https://lzone.de/cheat-sheet/Redis%20Sentinel)
