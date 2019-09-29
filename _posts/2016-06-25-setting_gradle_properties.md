---
title: "Setting gradle properties for Eclipse or Intellij IDEA"
layout: single
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'post tag-speeches'
comments: true
date: 2016-06-25 22:54:35 EDT
---

In our company, we have to use a proxy server to connect to our repository when working with VPN connection (which is terrible, but you just have to live with it!).

When we work on the command line, setting the proxy information in gradle.properties is working pretty well. However, when I tried to import the gradle project into Eclipse/Intellij Idea, the gradle.properties doesn't seem to be used. And what I ended up doing is to configure the properties into the JVM options. Just for later reference, I posted both of the two methods below:

## Settings in the gradle.properties

```
systemProp.ARTIFACTORY_URL=<YOUR_ARTIFACTORY_URL>
systemProp.ARTIFACTORY_USERNAME=<YOUR_USER_NAME>
systemProp.ARTIFACTORY_PASSWORD=<YOUR_USER_PASSWORD>

# Omit adding this part if you do not use VPN
systemProp.http.proxyHost=<PROXY_IP_ADDRESS>
systemProp.http.proxyPort=<PROXY_PORT>
systemProp.http.nonProxyHosts=localhost

systemProp.https.proxyHost=<PROXY_IP_ADDRESS>
systemProp.https.proxyPort=<PROXY_PORT>
systemProp.https.nonProxyHosts=localhost
```

## Setting in the JVM options for Gradle

In Eclipse or Intellij, when you import the gradle project, you have to configure the JVM options to get the project imported properly. The same options can be configured as the followings:

```bash
-DARTIFACTORY_URL=<YOUR_ARTIFACTORY_URL> -DARTIFACTORY_USERNAME=<YOUR_USER_NAME> -DARTIFACTORY_PASSWORD=<YOUR_USER_PASSWORD> -Dhttp.proxyHost=<PROXY_IP_ADDRESS> -Dhttp.proxyPort=<PROXY_PORT> -Dhttp.nonProxyHosts=localhost -Dhttps.proxyHost=<PROXY_IP_ADDRESS> -Dhttps.proxyPort=<PROXY_PORT> -Dhttps.nonProxyHosts=localhost
```

![Configure the gradle JVM options](/assets/images/gradle_jvm_options.png)

> Setting in Intellij IDEA is the same.


## Gradle home in Intellij

When import an existing gradle project to IDEA, sometimes you might want to use your local gradle installed via homebrew, to do that, you need to specify the GRADLE_HOME as following (for gradle 2.11):

```bash
/usr/local/Cellar/gradle/2.11/libexec/
```


