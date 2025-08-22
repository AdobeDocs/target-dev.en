---
title: Adobe Target Delivery API Overview
description: Adobe Target Delivery API Overview
keywords: delivery api
exl-id: e760bddc-b1ae-4b7b-bff2-aba81c6b6d34
feature: APIs/SDKs
---
# Delivery API overview

The [!DNL Adobe Target Delivery API] is based on REST. This documentation describes the resources that make up the [!DNL Adobe Target] [!DNL Delivery API]. HTTP methods are utilized to execute operations on those resources.

Using [!UICONTROL Adobe Target's Delivery API], you can:

* Deliver experiences across web, including SPAs, and mobile channels as well as non-browser based IoT devices such as a connected TV, kiosk, or in-store digital screen.
* Deliver experiences from any server side platform or application that can make HTTP/s calls.
* Deliver consistent and personalized experiences to a user no matter which channel or devices the user has engaged with your business.
* Cache experiences for a user within a session in your server so that multiple API calls can be avoided and as a result achieve better performance.
* Seamlessly integrate with [!DNL Adobe Experience Cloud] products such as [!DNL Adobe Analytics], [!DNL Adobe Audience Manager], and the [!DNL Experience Cloud ID Service] from the server side.

>[!IMPORTANT]
>
>Use caution when updating your [!DNL Recommendations] [!UICONTROL Catalog] via the [!DNL Delivery API]. The [!DNL Delivery API] is public, so avoid using it to populate clickable items in your recommendations catalog. Doing so can introduce invalidated content and pollute your catalog.
>
>Best Practices:
>
>Use the [!DNL Delivery API] only for updating catalog attributes that:
>* Change frequently (for example, price, stock level).
>* Follow a predefined format that can be easily validated on your website.
>* Do not use it for adding or modifying clickable items or other unverified content.
>
>If needed, you can request customer support to disable catalog updates through the Delivery API.

For more information, see the [[!UICONTROL Adobe Target Delivery API]](https://developer.adobe.com/target/implement/delivery-api/){target=_blank} documentation.

>[!NOTE]
>
>You can still access the [legacy /v1/mbox and /v2/batchmbox API documentation](https://developers.adobetarget.com/api/legacy-api/index.html). However, features will be developed in the Delivery API (as documented here) that will not be backported to the legacy APIs.
