---
title: Update profiles
description: Learn how to use Adobe Target Profile APIs to send visitor data to [!DNL Target].
contributors: https://github.com/icaraps
exl-id: 482a4175-1d02-47e9-a5c0-dd00e8560773
feature: APIs/SDKs
---
# Update profiles

A user profile contains demographic and behavioral information of a web page visitor, such as age, gender, products purchased, last time of visit, and so on. [!DNL Adobe Target] uses this information to personalize the content it serves to each visitor.

The profile information for each visitor is either stored in cookies or in third-party apps.

If your web page implements the [!DNL Target] code ([at.js](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md) or the [Adobe Experience Platform Web SDK](/help/dev/implement/client-side/aep-web-sdk.md)), the profile information from the cookies is passed to [!DNL Target] using profile parameters. [!DNL Target] identifies each visitor uniquely through a `pcID` that it generates in the visitor's cookies. However, you can pass profile parameters from an external app through mbox calls using `mbox3rdPartyIds`.

Use the [!DNL Adobe Target] profile APIs when you have profile data about your visitors to send to [!DNL Target] that you either can't or don't want to send as part of your page-based integration with [!DNL Target]. This might be data from a Customer Relationship Management (CRM) or Point of Sale (POS) system that isn't available on the page. Or this data might be of a more sensitive nature that does not make sense to pass on the page.

There are two ways to update profiles via API:

* [Single profile update API](/help/dev/administer/profile-api/profile-single-api.md)
* [Bulk profile update via batch](/help/dev/administer/profile-api/profile-bulk-api.md)
