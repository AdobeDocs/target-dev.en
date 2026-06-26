---
keywords: server side, server-side, api, sdk, node.js, nodejs, node js, recommendations api, api, apis, server side1
description: Learn about the [!DNL Adobe Target] server-side Delivery APIs, SDKs, and [!DNL Target Recommendations] APIs.
title: Where Can I Learn About [!DNL Target] Server-Side Delivery APIs and SDKs?
feature: Implement Server-side
exl-id: 3eb0a789-cf1a-4d02-acf7-3c895bcb662f
TQID: https://experienceleague.adobe.com/x5WKb9Eenz2bw-idOnxlpWdtiivTx05n38sNXEt3DNc
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: b050e0cd-2ddd-42cd-a71b-5d9e1fdf75e0
    internal-label: APIs and SDKs
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
    internal-label: Implementation
subfeature_v2:
  - id: a6cc21b9-1a36-4fa6-9c61-4acd04d9c88c
    internal-label: Delivery API
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
    internal-label: at.js
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
    internal-label: Measurement
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
    internal-label: Machine learning
---
# Server Side: implement [!DNL Target]

Information about [!DNL Adobe Target] server-side Delivery APIs, SDKs, and [!DNL Target Recommendations] APIs.

>[!NOTE]
>
>If your implementation uses at.js and [!DNL AppMeasurement] in client-side, you should use the [!UICONTROL Target Delivery API] and server-side SDKs discussed below.
>
>If your implementation uses the [!UICONTROL Adobe Experience Platform Web SDK], you should use the [[!UICONTROL Adobe Experience Platform] [!UICONTROL Edge Network Server API]](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network-server-api/overview){target=_blank}.

The following process occurs in a server-side implementation of [!DNL Target]:

1. A client device makes a request for an experience through your server.
1. Your server sends that request to [!DNL Target].
1. [!DNL Target] sends the response back to your server.
1. Your server makes the decision on which experience to deliver to the client device for it to render.

The experience does not need to display in a browser. The experience can display in an email or kiosk, via a voice assistant, or through some other non-visual experience or non-browser-based device. Because your server sits between the client and [!DNL Target], this type of implementation is also ideal if you need greater control and security or have complex backend processes that you want to run on your server.

>[!NOTE]
>
>A first-time visitor can be initialized only on the client-side. A first-time visitor *cannot* be initialized on the server-side. This is due to the ECID, which depends on the third-party demdex cookie and therefore needs to be initialized via Visitor API.js on an implementation where the browser is involved.

The following sections provide more information about the various server side APIs and SDKs:

## Server Side Delivery APIs

Link: [Server Side Delivery APIs](/help/dev/implement/delivery-api/overview.md)

`/rest/v1/delivery`

Through the [!DNL Target] Delivery API, you can:

* Deliver experiences across web, including SPAs, and mobile channels as well as non-browser based IoT devices, such as connected TVs, kiosks, or in-store digital screens.
* Deliver experiences from any server-side platform or application that can make HTTP/s calls.
* Deliver consistent and personalized experiences to a visitor regardless of which channel or devices the visitor used to engage with your business.
* Cache experiences for a visitor within a session on your server so that multiple API calls can be avoided, which achieves better performance.
* Seamlessly integrate with Adobe Experience Cloud products, such as Adobe Analytics, Adobe Audience Manager (AAM), and the Experience Cloud ID Service from the server side.

## Server Side SDKs

The [!DNL Adobe Target] server-side SDK documentation helps you implement [!DNL Target] on your servers in your language of choice.

* [Node.js](node-js/overview.md)
* [Java](java/overview.md)
* [.NET](net/overview.md)
* [Python](python/overview.md)

Through [!DNL Adobe Target]'s server-side SDKs, you can:

* Execute and run **feature flagging**, **rollouts**, and **A/B experiments** at **near-zero latency**.
* Deliver experiences across **web**, including **SPAs**, and **mobile channels**, as well as non-browser based **Internet of Things (IoT) devices** such as a connected TV, kiosk, or in-store digital screen.
* Deliver **Machine Learning (ML) driven personalized experiences** to a user, no matter which channel or device the user has engaged with your business.
* **Seamlessly integrate with Adobe Experience Cloud** products such as **Adobe Analytics**, **Adobe Audience Manager**, and the **Experience Cloud ID Service** from the server side.

See the [Getting Started](sdk-guides/getting-started/getting-started.md) page to learn how to run a simple feature flagging use case via [on-device decisioning](sdk-guides/on-device-decisioning/overview.md).

Check out our [Sample Apps](sdk-guides/sample-apps/sample-apps.md) to have fun and play around!

## [!DNL Target Recommendations] APIs

Link: [Target Recommendations APIs](https://developers.adobetarget.com/api/recommendations) and [Adobe Recommendations API Overview](../../before-administer/recs-api/overview.md).

The Recommendations APIs let you programmatically interact with [!DNL Target] recommendations servers. These APIs can be integrated with a range of application stacks to perform functions that you would typically do via the [!DNL Target] user interface.

## [!DNL Platform Edge Network] API calls without an SDK {#platform-edge-api-user-agent}

The [!UICONTROL Adobe Experience Platform Web SDK] and other supported SDK integrations include a browser-like `User-Agent` value in the HTTP request headers when calling the [!DNL Experience Platform Edge Network]. Server-side integrations that use the public [Interact API](https://experienceleague.adobe.com/en/docs/experience-platform/edge-network/server-api/interact){target=_blank} without an SDK must supply this header explicitly.

For non-SDK Interact API calls, observe the following requirements:

* Include a valid, browser-like `User-Agent` in the HTTP request headers. A visitor or user-agent value in the JSON request body alone does not meet bot-detection requirements for this integration pattern.
* Do not use placeholder or non-browser values, for example, `PHX/1.0`, such values can result in bot classification.
* An SDK name or SDK version is not required for public Edge API calls. For this scenario, a valid `User-Agent` HTTP header is the required element.

When [!DNL Target] classifies a request as bot traffic, personalization can fail or look intermittent because profile lookup, segment evaluation, and personalized content for activities such as [!UICONTROL Recommendations] and [!UICONTROL Auto-Target] are suppressed, as described below. 

Learn more about implementing with the SDK in the [[!DNL Adobe Experience Platform Web SDK] overview](https://experienceleague.adobe.com/en/docs/target-dev/developer/client-side/aep/aep-web-sdk-overview){target=_blank}.

**Example of Interact API request (headers must include `User-Agent`):**

```http
POST https://edge.adobedc.net/ee/v2/interact?dataStreamId=YOUR_DATASTREAM_ID&requestId=YOUR_REQUEST_ID
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/605.1.15 (KHTML, like Gecko) Version/26.5 Safari/605.1.15
Accept: */*
Content-Type: text/plain; charset=UTF-8
```
