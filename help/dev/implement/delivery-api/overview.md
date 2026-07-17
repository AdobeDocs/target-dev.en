---
title: Adobe Target Delivery API Overview
description: Adobe Target Delivery API Overview
keywords: delivery api
exl-id: e760bddc-b1ae-4b7b-bff2-aba81c6b6d34
feature: APIs/SDKs
TQID: https://experienceleague.adobe.com/gPXGax6ccvZZPklT3jnZbqyOj3mCClEfSpdufAFPtSs
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
---
# Delivery API overview

The [!DNL Adobe Target Delivery API] is based on REST. This documentation describes the resources that make up the [!DNL Adobe Target] [!DNL Delivery API]. HTTP methods are utilized to execute operations on those resources.

>[!IMPORTANT]
>
>The [!DNL Delivery API] documented here is intended for [!DNL at.js] and direct server-side implementations. If you are implementing [!DNL Target] using the [!DNL Adobe Experience Platform Web SDK], use the Interact API, accessed through the `sendEvent` command over the [!UICONTROL Experience Platform Edge Network],  instead of calling the [!DNL Delivery API] directly. See [Adobe Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md) and [Compare the at.js library to the Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk/web-sdk-atjs-comparison.md) for more information.

Using [!UICONTROL Adobe Target's Delivery API], you can:

* Deliver experiences across web, including SPAs, and mobile channels as well as non-browser based IoT devices such as a connected TV, kiosk, or in-store digital screen.
* Deliver experiences from any server side platform or application that can make HTTP/s calls.
* Deliver consistent and personalized experiences to a user no matter which channel or devices the user has engaged with your business.
* Cache experiences for a user within a session in your server so that multiple API calls can be avoided and as a result achieve better performance.
* Seamlessly integrate with [!DNL Adobe Experience Cloud] products such as [!DNL Adobe Analytics], [!DNL Adobe Audience Manager], and the [!DNL Experience Cloud ID Service] from the server side.

>[!NOTE]
>
>You can still access the [legacy /v1/mbox and /v2/batchmbox API documentation](https://developers.adobetarget.com/api/legacy-api/index.html). However, features will be developed in the Delivery API (as documented here) that will not be backported to the legacy APIs.
