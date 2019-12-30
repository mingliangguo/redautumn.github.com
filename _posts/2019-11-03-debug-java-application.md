---
title: "Debug java application"
layout: single
cover: false
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'posts'
comments: true
date: 2019-11-03 20:48:52 EST
---

Just use this post to write down some techniques about debugging java applications, especially for multi-thread, deadlock or memory issues.

For IBM JDK, use the following command to trigger thread dump.

```bash
kill -3 pid
```

For Open JDK

```bash
jps
jstack
```

## Tools for debugging http services

- [http toolkit](https://httptoolkit.tech/mock/)
  - Intercept & view all your HTTP(S)
  - Mock endpoints or entire servers
  - Rewrite, redirect, or inject errors

### State of Java threads

> There will be a lot of threads that will be irrelevant in 90% of cases. Focus on the threads where your application work occurs, such as the WebContainer thread pool. In this example, all of the threads are waiting for work (either parked in the WAS BoundedBuffer or in IBM AIO code waiting for the next event). Remember that only the full stack is meaningful. In some cases, a parked thread, or a thread waiting in Object.wait may be a problem, so it's best to look methodically through the stacks.
> - https://publib.boulder.ibm.com/httpserv/cookbook/Major_Tools-IBM_Thread_and_Monitor_Dump_Analyzer_TMDA.html


## References

- [How to read a thread dump](https://dzone.com/articles/how-to-read-a-thread-dump)
- [IBM Thread and Monitor Dump Analyzer for Java](https://www.ibm.com/support/knowledgecenter/en/SSLLVC_5.0.0/com.ibm.esupport.tool.tmda.doc/docs/readme.htm)


