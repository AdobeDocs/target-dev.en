---
title: Implement proxy configuration in the [!DNL Adobe Target] Java SDK
description: Learn how to configure the TargetClient proxy configuration in the [!DNL Adobe Target] Java SDK.
feature: APIs/SDKs
exl-id: 32e8277d-3bba-4621-b9c7-3a49ac48a466
---
# Proxy Configuration (Java)

## Basic Proxy

If the application running the SDK requires a proxy to access the internet, the `TargetClient` will need to be configured with a proxy configuration as follows.

### Basic Proxy Config

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .proxyConfig(new ClientProxyConfig(host,port))
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```

## Authentication

If a proxy authentication is required, the credentials can be passed as parameters to the `ClientProxyConfig` constructor, as per the below example. Note that this only works for simple username/password proxy authentication.

### Basic Proxy Authentication

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
    .client("acmeclient")
    .organizationId("1234567890@AdobeOrg")
    .proxyConfig(new ClientProxyConfig(host,port,username,password))
    .build();
TargetClient targetClient = TargetClient.create(clientConfig);
```

## On-device decisioning

For requests to fetch the rules artifact, your proxy should be configured to not cache the response. However, if it is not possible to configure the proxy's caching mechanism for that request, use a configuration option as a workaround to bypass the proxy-level cache. This workaround adds the `Authorization` header with an empty string value to the rules request, which should indicate to the proxy that the response should not be cached.  

In order to enable this workaround, set the following:

```java {line-numbers="true"}
ClientConfig.builder()
    .shouldArtifactRequestBypassProxyCache(true)
    .build();
```


