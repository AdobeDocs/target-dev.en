---
title: Adobe Analytics for Target (A4T) Logging in the Experience Platform Web SDK
description: Learn how to control the collection of Adobe Analytics for Target (A4T) data using the Experience Platform Web SDK.
seo-title: Adobe Analytics for Target (A4T) Logging in the Experience Platform Web SDK
seo-description: Learn how to control the collection of Adobe Analytics for Target (A4T) data using the Experience Platform Web SDK.
keywords: a4t;logging;analytics;sdk;web sdk;
feature: Implementation
---
# [!DNL Adobe Analytics for Target] (A4T) logging in the [!DNL Experience Platform Web SDK]

When using [!DNL Adobe Target] for personalization, you can choose which system you want to use for performance measurement. Each [Target activity](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html) allows you to select between [!DNL Target] reporting and Adobe [!DNL Analytics] reporting. 

If you are using [!DNL Analytics] reporting, [!DNL Target] has to communicate the following to [!DNL Analytics]:

* Which [!DNL Target] activity your visitors have entered
* Which experience they have seen
* Which conversion has been reached

The [!DNL Adobe Experience Platform Web SDK] supports two types of [!DNL Analytics] logging for [!UICONTROL Analytics for Target] (A4T) use cases:

| Logging method | Description |
| --- | --- |
| Server-side [!DNL Analytics] logging | All [!DNL Analytics] hits sent through the Edge Network are augmented with [!DNL Target] details on the server side, without having to go through the hit stitching process.  | 
| Client-side [!DNL Analytics] logging | [!DNL Target] data is returned on the client side, allowing you to manually augment and send data to [!DNL Analytics] using the [Data Insertion API](https://experienceleague.adobe.com/docs/analytics/import/c-data-insertion-api.html).| 

The logging method is determined by whether you have [!DNL Adobe Analytics] enabled on your configured [datastream](https://experienceleague.adobe.com/en/docs/experience-platform/datastreams/overview):

![Logging method decision flow](/help/dev/implement/a4t/assets/analytics-logging.png)

## Next steps

This document provided a brief introduction to the different logging methods for A4T data in the Web SDK. For more detailed information on each of these methods, refer to the following documentation:

* [Server-side logging for A4T data in the Experience Platform Web SDK](/help/dev/implement/a4t/client-side-logging.md)
* [Client-side logging for A4T data in the Experience Platform Web SDK](/help/dev/implement/a4t/client-side-logging.md)