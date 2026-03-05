---
title: Initialize the [!DNL Adobe Target] Java SDK to log requests
description: Learn how to log requests in the [!DNL Adobe Target] Java SDK.
feature: APIs/SDKs
exl-id: 85d1a6ef-0b08-4948-8133-740b7d6141dd
TQID: https://experienceleague.adobe.com/xvduuV6cjVJu-yIoaxCvbPE-ZttfEViuM8B7sVczAC0
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
    internal-label: Implementation
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
---
# Logger (Java)

## Description

When [initializing the SDK](initialize-sdk.md), there are several options on the `ClientConfig` object, which can be set to log requests.

|Option|Description|
| --- | --- |
|`logRequests`|Logs whole request body as well as response body.|
|`logRequestStatus`|Logs request's url, status along with response time.|

[!DNL Target] Java SDK uses `slf4j` logging. You need to provide your implementation of logger such as `java.util.logging`, `logback`, and `log4j`. Refer to [https://www.slf4j.org/manual.html](https://www.slf4j.org/manual.html) for more information. All logs will be printed in `debug`.

## Example

Add the `slf4j` dependency.

>[!BEGINTABS]

>[!TAB Gradle]

### Gradle

```javascript {line-numbers="true"}
compile 'org.slf4j:slf4j-simple:2.0.0-alpha0'
```

>[!TAB Maven]

```javascript {line-numbers="true"}
<dependency>
    <groupId>org.slf4j</groupId>
    <artifactId>slf4j-simple</artifactId>
    <version>2.0.0-alpha0</version>
</dependency>
```

>[!ENDTABS]

Enable the `DEBUG` logs based on your implementation, and mark the request logging flags.

### Debug

```javascript {line-numbers="true"}
System.setProperty(SimpleLogger.DEFAULT_LOG_LEVEL_KEY, "DEBUG");
ClientConfig config = ClientConfig.builder()
        .client("acmeclient")
        .organizationId("1234567890@AdobeOrg")
        .logRequests(true)
        .logRequestStatus(true)
        .build();

TargetClient targetClient = TargetClient.create(config);
```

You should see requests, responses, and response times being printed in the console.
