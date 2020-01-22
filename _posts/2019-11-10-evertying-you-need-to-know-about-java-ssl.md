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

### Working with Certificates and SSL

> Installation of the Application Server generates a digital certificate in JSSE (Java Secure Socket Extension) format suitable for internal testing. By default, the Application Server stores its certificate information in two files in the domain-dir/config directory:
>
> Keystore file, keystore.jks, contains the Application Server’s certificate, including its private key. The keystore file is protected with a password, initially changeit. Change the password using keytool. For more information about keytool, read Using the keytool Utility.
>
> Each keystore entry has a unique alias. After installation, the Application Server keystore has a single entry with alias s1as.
>
> Truststore file, cacerts.jks, contains the Application Server’s trusted certificates, including public keys for other entities. For a trusted certificate, the server has confirmed that the public key in the certificate belongs to the certificate’s owner. Trusted certificates generally include those of certification authorities (CAs).
>
> In the Platform Edition, on the server side, the Application Server uses the JSSE format, which uses keytool to manage certificates and key stores. In the Enterprise Edition, on the server side, the Application Server uses NSS, which uses certutil to manage the NSS database which stores private keys and certificates. In both editions, the client side (appclient or stand-alone), uses the JSSE format.
>
> By default, the Application Server is configured with a keystore and truststore that will work with the example applications and for development purposes. For production purposes, you may wish to change the certificate alias, add other certificates to the truststore, or change the name and/or location of the keystore and truststore files.

### Truststore v.s. keystore

- https://www.baeldung.com/java-keystore-truststore-difference

### Stackoverflow answer

- https://stackoverflow.com/questions/6340918/trust-store-vs-key-store-creating-with-keytool

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

So the following JVM arguments can be used to specify the truststore or keystore:

```bash
-Djavax.net.ssl.trustStore=/path/to/your_trustStore.jks -Djavax.net.ssl.trustStorePassword=somepassword
-Djavax.net.ssl.keystore=/path/to/your_keyStore.jks -Djavax.net.ssl.keyStorePassword=somepassword

````

### Helper commands

```bash
# to capture a certificate from a server
echo q | openssl s_client -showcerts -connect (hostname):(port)
```

## References

- https://www.ibm.com/support/knowledgecenter/SS7K4U_liberty/com.ibm.websphere.wlp.zseries.doc/ae/twlp_add_trust_cert.html
- [Everything About HTTPS and SSL (Java)](https://dzone.com/articles/ssl-in-java)
