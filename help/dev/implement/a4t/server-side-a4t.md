---
title: Server-side logging for A4T data in Experience Platform Web SDK
description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
seo-title: Server-side logging for A4T data in Experience Platform Web SDK
seo-description: Learn how to enable server-side logging for Adobe Analytics for Target (A4T) using the Experience Platform Web SDK.
keywords: a4t;target;web;sdk;platform;logging;
feature: Implementation
exl-id: 716f7343-69a6-44d7-baec-a0a0df1b6e1f
TQID: https://experienceleague.adobe.com/I7-G2VO2AN3qFsgkk4JX2Pg6WJfZq0HZkcGL4XQNoWg
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
# Server-side logging for A4T data in [!DNL Experience Platform Web SDK]

The [!DNL Adobe Experience Platform Web SDK] allows you to implement [!UICONTROL Adobe Analytics for Target] (A4T) functionality on [!UICONTROL Experience Platform Edge Network]. When server-side logging is enabled, all [!DNL Analytics] hits sent through the Edge Network are augmented with [!DNL Target] details on the server side, without having to go through the hit stitching process. 

Server-side logging for [!DNL Analytics] is enabled when [!DNL Analytics] is enabled in the datastream configuration:

![Analytics datastream configuration enabled](/help/dev/implement/a4t/assets/enable-analytics-datastream.png)

The following diagram shows how data flows through the system when server-side [!DNL Analytics] Logging is enabled:

![Server-side logging flow](/help/dev/implement/a4t/assets/analytics-server-side-logging.png)

## Next steps

This guide covered server-side logging for A4T data in the Web SDK. See the guide on [client-side logging](/help/dev/implement/a4t/client-side-logging.md) for more information on how to handle A4T data on the client side.
