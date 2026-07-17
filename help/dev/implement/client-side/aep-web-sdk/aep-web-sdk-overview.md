---
keywords: Adobe Experience Platform Web SDK, aep web sdk, web sdk, sdk, adobe experience cloud, platform edge network, adobe experience platform edge network, edge network, aep edge network, Adobe Experience Platform Web SDK0
description: Learn how to use the [!UICONTROL Adobe Experience Platform Web SDK] to interact with the various services in the [!UICONTROL Adobe Experience Cloud] through the [!UICONTROL AEP Edge Network].
title: How Do I Implement with the [!UICONTROL Experience Platform Web SDK]?
feature: AEP Web SDK
exl-id: 35ee60d2-3d6d-4169-9f22-b2aef4c6548b
TQID: https://experienceleague.adobe.com/j3-KSuCkcyyTB2KG4Icm2E7xpAfcuPkaOlhxitd5q-4
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
    internal-label: Audiences
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
    internal-label: Implementation
  - id: f7c7de77-382f-4f48-8b36-61a170f06d3d
    internal-label: Integrations
subfeature_v2:
  - id: df62f171-ac37-440f-8f0f-f41a72ebdd34
    internal-label: Analytics integration
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
    internal-label: at.js
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
---
# [!UICONTROL Adobe Experience Platform Web SDK]

[!UICONTROL Adobe Experience Platform Web SDK] (AEP Web SDK) is a client-side JavaScript library that allows customers of [!UICONTROL Adobe Experience Cloud] to interact with the various services in the [!DNL Adobe Experience Cloud] (including [!DNL Target]) through the [!UICONTROL Adobe Experience Platform Edge Network]. In addition to the JavaScript library, there is an [!UICONTROL Adobe Experience Platform] extension to help with your Web SDK configurations.

>[!IMPORTANT]
>
>When implementing [!DNL Target] with the [!UICONTROL Adobe Experience Platform Web SDK], requests and responses go through the Interact API (via the `sendEvent` command over the [!UICONTROL Experience Platform Edge Network]), not the [!DNL Target] [Delivery API](/help/dev/implement/delivery-api/overview.md). The [!DNL Delivery API] is intended for [!DNL at.js] and direct server-side implementations only. See [Compare the at.js library to the Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk/web-sdk-atjs-comparison.md) to understand how the two approaches differ.

For more information, see the following links in the *[!UICONTROL Adobe Experience Platform Web SDK]* help:

* For comprehensive information: [What is [!UICONTROL Adobe Experience Platform Web SDK]](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html)
* For information specific to [!DNL Target]: [[!DNL Target] Overview](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/target-overview.html)

## Tutorials

The following tutorials help you  with your implementation:

### Implement [!DNL Adobe Experience Cloud] with [!DNL Platform Web SDK]

Learn how to implement [!DNL Experience Cloud] applications using [!DNL Adobe Experience Platform Web SDK] with [this tutorial](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/overview.html). For information specific to [!DNL Target], see the tutorial section titled [Set up [!DNL Target] with Platform Web SDK](https://experienceleague.adobe.com/docs/platform-learn/implement-web-sdk/applications-setup/setup-target.html).

### Migrate [!DNL Target] from at.js 2.*x* to [!DNL Platform Web SDK]

Learn how to migrate your [!DNL Target] implementation from at.js 2.*x* to the [!DNL Adobe Experience Platform Web SDK] with [this tutorial](https://experienceleague.adobe.com/docs/platform-learn/migrate-target-to-websdk/introduction.html).

## Recommended documentation

In addition to the [!UICONTROL Platform Web SDK] documentation mentioned above, topics in this guide also have information specific to the [!UICONTROL Platform Web SDK] as it relates to [!DNL Target] features and functionality.

|Feature|Description/Link|
| --- | --- |
|[Activity QA](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html)|Use QA URLs in [!DNL Target] to perform easy end-to-end activity QA with preview links that never change, optional audience targeting, and QA reporting that stays segmented from live activity data. Activity QA lets you fully test your [!DNL Target] activities before launching them live.<p>See [Target JavaScript library QA Mode compatibility](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html#compatibility) and [Preview URLs](https://experienceleague.adobe.com/docs/target/using/activities/activity-qa/activity-qa.html#preview).|
|[[!UICONTROL Analytics for Target] (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html)| [!UICONTROL Adobe Analytics for Target] (A4T) is a cross-solution integration that lets you create activities based on [!DNL Analytics] conversion metrics and audience segments. The A4T integration lets you use Analytics reports to examine your results.<p>See [Supported activity types](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html#section_F487896214BF4803AF78C552EF1669AA) and [Implementation steps for an Adobe Experience Platform Web SDK implementation](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4timplementation.html#platform).|
|[Audiences](https://experienceleague.adobe.com/docs/target/using/audiences/target.html)|Audiences in [!DNL Target] determine who sees content and experiences in a targeted activity.<p>See [Use the Audiences list](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html#use-list) and [Combine multiple audiences](https://experienceleague.adobe.com/docs/target/using/audiences/combining-multiple-audiences.html).|
|[Create audiences](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html)|Using audiences created in [!DNL Adobe Experience Platform] provide richer customer data that leads to more impactful personalization.<p>See [Use audiences from Adobe Experience Platform](https://experienceleague.adobe.com/docs/target/using/audiences/create-audiences/audiences.html#aep).|
|[Offer decisions](https://experienceleague.adobe.com/docs/target/using/integrate/ajo/offer-decision.html)|Add offer decisions created in [!DNL Adobe Journey Optimizer] to [!DNL Target] activities (manual A/B Test or Experience Targeting) to determine and deliver the next best offer for your visitors on web and mobile.|
|[Redirect offers - A4T FAQ](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html)|Redirect offers cause visitors' browsers to redirect to a new page.<p>See [Does the [!UICONTROL Adobe Experience Platform Web SDK] support redirect offers for A4T?](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t-faq/a4t-faq-redirect-offers.html#platform)|
|[Response tokens](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html)|Response tokens let you send [!DNL Target] data to Google Analytics and other 3rd-party integrations.<p>See [Sending data to Google Analytics via Platform Web SDK](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html#sending-data-to-google-analytics-via-platform-web-sdk) to see a code sample of how to accomplish this task.|
|[Single-page application implementation](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/adobe-target/spa-implementation.html) in the *[!UICONTROL Platform Web SDK] overview* guide. |[!UICONTROL Adobe Experience Platform Web SDK] provides rich features that equip your business to execute personalization on next-generation, client-side technologies such as single-page applications (SPAs).|
|[TLS (Transport Layer Security) encryption changes](/help/dev/before-implement/tls-transport-layer-security-encryption.md)|TLS (Transport Layer Security) helps you maintain the highest security standards and promote the safety of customer data.|
