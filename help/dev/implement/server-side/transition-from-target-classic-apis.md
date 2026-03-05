---
keywords: api, adobe i/o, classic, adobe developer console
description: Learn how to transition from the [!DNL Adobe Target Classic] APIs to the [!DNL Target] APIs on the [!DNL Adobe Developer Console].
title: How Do I Transition From [!DNL Target Classic] APIs to [!DNL Target] APIs on the [!DNL Adobe Developer Console]?
feature: APIs/SDKs
exl-id: b84e3767-89ad-4e2d-9bb4-7e31bffbc285
TQID: https://experienceleague.adobe.com/cIWcraU0O9Ut1VBbD5ScKOyBrXniyIEM5XEVZMJvffk
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
    internal-label: Implementation
  - id: f7c7de77-382f-4f48-8b36-61a170f06d3d
    internal-label: Integrations
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
    internal-label: Customer experience
---
# Transition from [!DNL Target Classic] APIs to [!DNL Target] APIs on the [!DNL Adobe Developer Console]

Information to help you transition from the [!DNL Target Classic] APIs to the [!DNL Target] APIs on the [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/home).

With the decommissioning of [!DNL Adobe Target Classic], the APIs connected to your [!DNL Target Classic] account have also been made unavailable. This article will help you transition your [!DNL Target Classic] API-based integrations to the [!DNL Target] APIs powered by the [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/home).

For more information about [!DNL Target] APIs, see [[!DNL Target] APIs](/help/dev/before-administer/target-api-overview.md). For more information about [!DNL Target] SDKs, see [[!DNL Target] Server-side Implementation](/help/dev/implement/server-side/server-side-overview.md)

## Terminology

| Term | Description |
|--- |--- |
|Classic API|APIs that are linked to your [!DNL Target Classic] account. These API calls are based on a username and password-based authentication and use the hostname `testandtarget.omniture.com`. If your API calls contain a user name and password in the request URL, you must transition to the [!DNL Adobe Developer Console] APIs.|
|[[!DNL Adobe Developer Console]](https://developer.adobe.com/console/home)|The [!DNL Adobe Developer Console] is the gateway for [!DNL Target] APIs. These APIs are connected to your [!DNL Target Standard/Premium] account. The [!DNL Target] APIs on the [!DNL Adobe Developer Console] use a [JWT-based authentication](../../before-administer/configure-authentication.md), which is the industry standard for secure enterprise APIs.|

## Timeline

The following APIs were decommissioned when [!DNL Target Classic] was decommissioned:

| Date | Details |
|--- |--- |
|October 17, 2017|All API methods that perform a write operation (`saveCampaign`, `copyCampaign`, `saveHTMLOfferContent`, and `setCampaignState`) were decommissioned.<P>This is the same date when all [!DNL Target Classic] user accounts were set to read-only status.|
|November 14, 2017|The remaining APIs were decommissioned. This is the date when the [!DNL Target Classic] user interface was decommissioned|

[!DNL Recommendations Classic] APIs were not impacted by this timeline.

## Equivalent Methods

The following table lists the equivalent [!DNL Adobe Developer Console] API methods for the Classic API methods. The [!DNL Adobe Developer Console] APIs return JSON, whereas the Classic APIs return XML.

The [!DNL Adobe Developer Console] API methods are linked to the corresponding section in the API documentation site. An example is provided for each API method. You can also use the [!DNL Target] Admin API Postman Collection that contains sample API calls for all the Adobe API methods on the [!DNL Adobe Developer Console].

| Grouping | Classic API Method | [!DNL Adobe Developer Console] API Method | Notes |
|--- |--- |--- |--- |
|Campaign/Activity|Campaign Create|[Create AB Activity](https://developers.adobetarget.com/api/#create-ab-activity)<P>[Create XT Activity](https://developers.adobetarget.com/api/#create-xt-activity)|The new APIs provide separate create methods for AB and XT|
||Campaign Update|[Update AB Activity](https://developers.adobetarget.com/api/#update-ab-activity)<P>[Update XT Activity](https://developers.adobetarget.com/api/#update-xt-activity)||
||Copy Campaign|N/A|Use the Activity Create APIs|
||Campaign List|[List Activities](https://developers.adobetarget.com/api/#list-activities)||
||Campaign State|[Update Activity State](https://developers.adobetarget.com/api/#update-activity-state)||
||Campaign View|[Get AB Activity by ID](https://developers.adobetarget.com/api/#get-ab-activity-by-id)<P>[Get XT Activity by ID](https://developers.adobetarget.com/api/#get-xt-activity-by-id)||
||Third-Party Campaign ID|N/A|If you are using a thirdpartyID, the relevant Activity methods can be used|
|Offers|Offer Create|[Create Offer](https://developers.adobetarget.com/api/#create-offer)||
||Offer Get|[Get Offer by ID](https://developers.adobetarget.com/api/#get-offer-by-id)||
||Offer List|[List Offers](https://developers.adobetarget.com/api/#list-offers)||
||Folder List|N/A|Folders aren't supported in [!DNL Target Standard/Premium]|
|Reporting|Campaign Performance Report|[Get AB Performance Report](https://developers.adobetarget.com/api/#get-ab-performance-report)<P>[Get XT Performance Report](https://developers.adobetarget.com/api/#get-xt-performance-report)||
||Audit Report|[Get Audit Report](https://developers.adobetarget.com/api/#get-audit-report)||
||1-1 Content Report|[Get AP Performance Report](https://developers.adobetarget.com/api/#get-ap-activity-performance-report)||
|Account Settings|Get Host Groups|[List Environments](https://developers.adobetarget.com/api/#list-environments)||

## Exceptions

If you require an exception, please contact your Customer Success Manager.

## Help

Please contact [!DNL Adobe Target Client Care] (tt-support@adobe.com) if you have any questions or need help transitioning from the Classic APIs to the [!DNL Target] APIs on the [!DNL Adobe Developer Console].
