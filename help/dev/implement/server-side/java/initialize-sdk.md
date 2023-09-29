---
title: Initialize the Java SDK using the create method
description: Learn how to use the create method to initialize the Java SDK and instantiate the [!UICONTROL TargetClient] to make calls to [!DNL Adobe Target] for experiments and personalized experiences.
feature: APIs/SDKs
exl-id: 0e0ddead-7de8-4549-b81c-e72598558e4b
---
# Initialize the Java SDK

## Description

Use the `create` method in order to initialize the Java SDK and instantiate the [!UICONTROL Target Client] to make calls to [!DNL Adobe Target] for experiments and personalized experiences.

## Method

[!UICONTROL TargetClient] is created using `TargetClient.create`.

### create

```javascript {line-numbers="true"}
TargetClient TargetClient.create(ClientConfig clientConfig)
```

ClientConfig is created using `ClientConfig.builder`.

```javascript {line-numbers="true"}
ClientConfigBuilder ClientConfig.builder()
```

## Parameters

`ClientConfigBuilder` has the following structure:

|Name|Type|Required|Default|Description|
| --- | --- | --- | --- | --- |
|client|String|Yes|None|[!UICONTROL Target Client Id]|
|organizationId|String|Yes|None|[!UICONTROL Experience Cloud Organization ID]|
|connectTimeout|Number|No|10000|Connection timeout for all requests in milliseconds|
|socketTimeout|Number|No|10000|Socket timeout for all requests in milliseconds|
|maxConnectionsPerHost|Number|No|100|Max Connections per [!DNL Target] host|
|maxConnectionsTotal|Number|No|200|Max Connections including all [!DNL Target] hosts|
|connectionTtlMs|Number|No|-1|Total time to live (TTL) defines maximum life span of persistent connections in milliseconds. By default connections will be kept alive indefinitely|
|idleConnectionValidationMs|Number|No|1000|Period of inactivity in milliseconds after which persistent connections are re-validated prior to being reused|
|evictIdleConnectionsAfterSecs|Number|No|20|The time in seconds to evict idle connections from the connection pool|
|enableRetries|Boolean|No|true|Automatic retries for socket timeouts (max 4)|
|logRequests|Boolean|No|false|Log [!DNL Target] requests and responses in debug|
|logRequestStatus|Boolean|No|false|Log [!DNL Target] response time, status, and URL|
|serverDomain|String|No|`*client*.tt.omtrdc.net`|Overrides default hostname|
|secure|Boolean|No|true|Unset to enforce HTTP scheme|
|requestInterceptor|HttpRequestInterceptor|No|Null|Add custom request Interceptor|
|defaultPropertyToken|String|No|None|Sets the default property token for every `getOffers` call. **For on-device decisioning**, the SDK will only download the artifact that contains the qualified activities for the property token set in `defaultPropertyToken`|
|defaultDecisioningMethod|DecisioningMethod enum|No|SERVER_SIDE|Must be set to ON_DEVICE or HYBRID to enable on-device decisioning|
|telemetryEnabled|Boolean|No|true|Allows customers to opt out of additional data collection during requests to [!DNL Target] servers|
|proxyConfig|ClientProxyConfig|No|None|Allows the client to provide their own proxy details|
|exceptionHandler|TargetExceptionHandler|No|None|Can be used to implement custom exception handling during rule processing|
|httpClient|HttpClient|No|None|Allows users to replace the [!DNL Target] HTTP client with a custom HTTP Client|
|onDeviceEnvironment|String|No|production|Can be used to specify a different on-device environment, such as staging|
|onDeviceConfigHostname|String|No|`assets.adobetarget.com`|Can be used to specify a different host to use to download the on-device decisioning artifact file|
|onDeviceDecisioningPollingIntSecs|int|No|300 (5 minutes)|Number of seconds between fetches of the on-device decisioning artifact file|
|onDeviceArtifactPayload|byte[]|No|None|Provides on-device decisioning with previous artifact payload to allow immediate execution|
|onDeviceDecisioningHandler|OnDeviceDecisioningHandler|No|None|Registers callbacks for on-device decisioning events|
|onDeviceAllMatchingRulesMboxes|List\<String\>|No|None|Allows users to specify mboxes for which all matching rule content will be returned during on-device decisioning|

## Example

### Java

```java {line-numbers="true"}
ClientConfig clientConfig = ClientConfig.builder()
        .client("acmeclient")
        .organizationId("1234567890@AdobeOrg")
        .build();

TargetClient.create(clientConfig);

// make calls to Adobe Target
```
