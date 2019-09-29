---
title: "TLSv1.2 Support in Java"
layout: single
categories: 'blog'
tags: 'blog'
navigation: True
subclass:
  - 'posts'
  - 'tag-speeches'
comments: true
date: 2019-09-07 11:43:08 EDT
---


## Some common errors related to SSL negotiation:

A lot of websites have dropped the TLSv1 support and requires TLSv1.2 or above. And this has caused a lot of problems for old Java applications. For Oracle JDK, `TLSv1.1` and `TLSv1.2` are enabled by default in Java 8. And for IBM JDK, it actually requires an additional parameter to enable `TLSv1.2` even on Java 8 - `-Dcom.ibm.jsse2.overrideDefaultTLS=true`.

If you see exceptions related to `SSLException`, it's very likely caused by the `TLS` issue.

> `javax.net.ssl.SSLException: Received fatal alert: protocol_version`

This error usually means the client and server has mismatch on the TLS versions. To check the TLS version the server supports. You can use the following command to check what's the supported TLS version and make sure your client code supports one of them.

```bash
openssl s_client -connect www.google.com:443
```

Or you can use this website to check: https://www.ssllabs.com/ssltest/viewMyClient.html

## Some configurations to enable TLSv1.2

- JVM args:

```
-Dhttps.protocols=TLSv1.2
-Djdk.tls.client.protocols=TLSv1.2
```

**NOTE*:*

`-Djdk.tls.client.protocols=TLSv1.2` seems less used than `-Dhttps.protocols=TLSv1.2`.

- Environment variables:

```bash
export JAVA_TOOL_OPTIONS="-Dhttps.protocols=TLSv1.2"
export JAVA_OPTS="-Dhttps.protocols=TLSv1.2 -Djdk.tls.client.protocols=TLSv1.2"
```

Both of the two environment variables are supported by Gradle.

- Code

Or you can do it equivalently in code:

```java
System.setProperty("https.protocols", "TLSv1,TLSv1.1,TLSv1.2");
// or
System.setProperty("https.protocols", "TLSv1.2");
```

Note for IBM JDK, there is a different parameter to enable TLSv1.2 support:

```
-Dcom.ibm.jsse2.overrideDefaultTLS=true
```

## Under the hood

The enabled `https protocols` are configured via [SSLSocket.setEnabledProtocols(String[]) ](https://docs.oracle.com/javase/8/docs/api/javax/net/ssl/SSLSocket.html#setEnabledCipherSuites-java.lang.String:A-) under the cover. If `URLConnection` is used underneath, then setting the `https.protocols` should just work. However, if a different library is used (e.g. apache httpclient), it might not work and you have to figure out what need to be configured to set `TLSv1.2` as enabled protocols.

For HttpClient `4.5.+`, the following code snippet will enable it for you:

```java
SSLConnectionSocketFactory sslConnectionSocketFactory =
    new SSLConnectionSocketFactory(SSLContexts.createDefault(),
           new String[] { "TLSv1.1", "TLSv1.2", "TLSv1.3" },
           null,
           SSLConnectionSocketFactory.getDefaultHostnameVerifier());

PoolingHttpClientConnectionManager connectionManager =
    new PoolingHttpClientConnectionManager(
        RegistryBuilder.<ConnectionSocketFactory> create()
          .register("http",
              PlainConnectionSocketFactory.getSocketFactory())
          .register("https",
              sslConnectionSocketFactory)
          .build());

HttpClient httpClient = HttpClientBuilder.create()
          .setConnectionManager(connectionManager)
          .build()

```

*Note*: The above approach doesn't require and will ignore the external configuration.  Instead of creating a custom connection manager, an alternative approach is to use [useSystemProperties](https://hc.apache.org/httpcomponents-client-ga/httpclient/apidocs/org/apache/http/impl/client/HttpClientBuilder.html#useSystemProperties()) , this works with the jvm arguments configured in the system. And the coding is actually much simpler.

```java
HttpClient httpClient = client = HttpClientBuilder
  .create()
  .useSystemProperties()
  .build();
```



Refer to the discussion here: https://stackoverflow.com/questions/28391798/how-to-set-tls-version-on-apache-httpclient


## Debugging

Enable the following JVM args to enable debug logs.

```
-Djavax.net.debug=all
```

For gradle tasks, the standard outputstream is not logged by default, you can turn it on by following this link: https://docs.gradle.org/current/dsl/org.gradle.api.tasks.testing.logging.TestLoggingContainer.html


The other helpful resources:

- https://blogs.oracle.com/pdit-cas/all-you-need-to-know-about-tlsv12
