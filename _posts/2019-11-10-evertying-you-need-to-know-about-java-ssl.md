---
title: "Evertying you need to know about Java SSL"
layout: single
cover: false
categories: 'blog'
tags: 'blog'
navigation: True
subclass: 'posts'
comments: true
date: 2019-11-10 19:52:00 EST
---

## Truststore v.s. Keystore

- https://www.baeldung.com/java-keystore-truststore-difference

- Stackoverflow answer: https://stackoverflow.com/questions/6340918/trust-store-vs-key-store-creating-with-keytool

>  The terminology is a bit confusing indeed, but both javax.net.ssl.keyStore and javax.net.ssl.trustStore are used to specify which keystores to use, for two different purposes. Keystores come in various formats and are not even necessarily files (see this question), and keytool is just a tool to perform various operations on them (import/export/list/...).
>
> The javax.net.ssl.keyStore and javax.net.ssl.trustStore parameters are the default parameters used to build KeyManagers and TrustManagers (respectively), then used to build an SSLContext which essentially contains the SSL/TLS settings to use when making an SSL/TLS connection via an SSLSocketFactory or an SSLEngine. These system properties are just where the default values come from, which is then used by SSLContext.getDefault(), itself used by SSLSocketFactory.getDefault() for example. (All of this can be customized via the API in a number of places, if you don't want to use the default values and that specific SSLContexts for a given purpose.)
>
> The difference between the KeyManager and TrustManager (and thus between javax.net.ssl.keyStore and javax.net.ssl.trustStore) is as follows (quoted from the JSSE ref guide):
>
> TrustManager: Determines whether the remote authentication credentials (and thus the connection) should be trusted.
>
> KeyManager: Determines which authentication credentials to send to the remote host.
>
> (Other parameters are available and their default values are described in the JSSE ref guide. Note that while there is a default value for the trust store, there isn't one for the key store.)
>
> Essentially, the keystore in javax.net.ssl.keyStore is meant to contain your private keys and certificates, whereas the javax.net.ssl.trustStore is meant to contain the CA certificates you're willing to trust when a remote party presents its certificate. In some cases, they can be one and the same store, although it's often better practice to use distinct stores (especially when they're file-based).
