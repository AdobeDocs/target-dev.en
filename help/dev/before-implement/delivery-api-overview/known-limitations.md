---
title: Adobe Target Delivery API considerations and known limitations
description: What considerations and known limitations should I consider when using the [!UICONTROL Adobe Target Delivery API]?
keywords: delivery api
exl-id: 49fe13b0-efcb-4b1c-a4cb-03b64fbd9214
feature: APIs/SDKs
---
# Considerations and known limitations

The following information lists considerations and known limitations with using the [!DNL Adobe Target] [!DNL Delivery API].

* There is no authentication for [!DNL Target] Delivery APIs.
* This API does not process cookies or redirect calls.
* Both HTTP/1.1 and HTTP/2 header names are case-insensitive; however, HTTP/2 enforces lowercase header names. For more information, see the [Hypertext Transfer Protocol Version 2 (HTTP/2) documentation](https://www.rfc-editor.org/rfc/rfc7540#section-8.1.2){target=_blank}.

  If you use an endpoint that routes visitors through our new Load Balancer infrastructure, their connections are automatically upgraded to HTTP/2. This upgrade process converts request headers to lowercase headers so they won't be considered malformed.

  This issue can potentially be an issue for customers if their libraries are set up to look for case-sensitive (specifically not lower-case) request/response headers.

* Use caution when updating your [!DNL Recommendations] [!UICONTROL Catalog] via the [!DNL Delivery API]. The [!DNL Delivery API] is public, so avoid using it to populate clickable items in your recommendations catalog. Doing so can introduce invalidated content and pollute your catalog.

  **Best Practices**:

  Use the [!DNL Delivery API] only for updating catalog attributes that:
  * Change frequently (for example, price, stock level).
  * Follow a predefined format that can be easily validated on your website.
  * Do not use it for adding or modifying clickable items or other unverified content.
  * If needed, you can request customer support to disable catalog updates through the Delivery API.

  For more information, see the [[!UICONTROL Adobe Target Delivery API]](https://developer.adobe.com/target/implement/delivery-api/){target=_blank} documentation.
