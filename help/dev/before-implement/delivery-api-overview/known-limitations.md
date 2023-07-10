---
title: Adobe Target Delivery API considerations and known limitations
description: What considerations and known limitations should I consider when using the [!UICONTROL Adobe Target Delivery API]?
keywords: delivery api
exl-id: 49fe13b0-efcb-4b1c-a4cb-03b64fbd9214
---
# Considerations and known limitations

* There is no authentication for [!DNL Target] Delivery APIs.
* This API does not process cookies or redirect calls.
* Support for [!UICONTROL Automated Personalization] (AP) and [!UICONTROL Recommendations] activities: This API has two modes for fetching content: execute and prefetch mode. Prefetch mode can only be used for [!UICONTROL AB Test] and [!UICONTROL Experience Targeting] (XT) activities. Do not use prefetch mode for [!UICONTROL Automated Personalization] (AP), [!UICONTROL Auto-Allocate], [!UICONTROL Auto-Target], or [!UICONTROL Recommendations] activity types.
* Both HTTP/1.1 and HTTP/2 header names are case-insensitive; however, HTTP/2 enforces lowercase header names. For more information, see the [Hypertext Transfer Protocol Version 2 (HTTP/2) documentation](https://www.rfc-editor.org/rfc/rfc7540#section-8.1.2){target=_blank}.

  If you use an endpoint that routes visitors through our new Load Balancer infrastructure, their connections are automatically upgraded to HTTP/2. This upgrade process converts request headers to lowercase headers so they won't be considered malformed.

  This issue can potentially be an issue for customers if their libraries are set up to look for case-sensitive (specifically not lower-case) request/response headers.
