---
title: Install the Java SDK
description: Learn how t install the [!DNL Adobe Target] Java SDK.
feature: APIs/SDKs
exl-id: 5828d5b3-c487-49bf-9458-7ef94374e32d
---
# Install the Java SDK

The Java SDK is distributed by [Maven Central](https://search.maven.org/artifact/com.adobe.target/target-java-sdk). To get started, add it as a dependency by installing in `gradle` or `maven`:

>[!BEGINTABS]

>[!TAB Gradle]

```javascript {line-numbers="true"}
compile 'com.adobe.target:java-sdk:1.0'
```

>[!TAB Maven]

```javascript {line-numbers="true"}
<dependency>
    <groupId>com.adobe.target</groupId>
    <artifactId>java-sdk</artifactId>
    <version>2.0</version>
</dependency>
```

>[!ENDTABS]

The open sourced code can be found at <https://github.com/adobe/target-java-sdk>.
