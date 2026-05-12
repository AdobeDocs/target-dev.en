---
title: Adobe Target API Overview
description: Overview of the different Adobe Target APIs, including delivery api, reporting api, admin api, profile api, recommendations api, and links to postman collections.
exl-id: bf886103-36af-4061-b8be-2fe645f45ff3
feature: APIs/SDKs
TQID: https://experienceleague.adobe.com/GbrWhrZxH-sTtpxotpJGbr-sHuIXrX7rZFQhju76-vM
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
    internal-label: Audiences
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
    internal-label: Implementation
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
---
# Target API overview

This article describes the different Target APIs in general, before focusing on requirements specific to the Admin and Profile APIs. If you wish to administer Target via the UI, see the [administration section of the *Adobe Target Business User Guide*](https://experienceleague.adobe.com/docs/target/using/administer/administrating-target.html?lang=en).

## API Types

The Adobe Target APIs are a collection of APIs that power Adobe Target products, such as Adobe Recommendations. These APIs allow for the creation of data-rich user interfaces you can use to manipulate and integrate data.

Adobe Target APIs may be grouped according to type: Admin, Profile, Delivery, and Reporting. 

>[!NOTE]
>
>The Admin APIs and Profile APIs are often referred to collectively ("Admin and Profile APIs"), but may also be referred to separately ("Admin APIs" and "Profile APIs"). The Recommendations API is a specific implementation of a Target Admin API.
 
|API type|What it enables you to do|Download link|Other helpful links|
| --- | --- | --- |--- |
|[Admin](../administer/admin-api/admin-api-overview-new.md)|Create, modify, and delete activities, audiences, offers, and other objects (including Recommendations entities, criteria, designs, and so on. The Recommendations APIs are a type of Admin API.)|<UL><li>[Target Admin API Postman Collection](https://developers.adobetarget.com/api/#admin-postman-collection)</li><li>[Recommendations API Postman Collection](https://developer.adobe.com/target/administer/recommendations-api/#section/Postman)</li></UL>|[Use Recommendations APIs](../before-administer/recs-api/overview.md)|
|Profile|Retrieve and modify user profiles stored in Adobe Target.|[Target Profile API Postman Collection](https://developers.adobetarget.com/api/#profiles)||
|[Delivery](../implement/delivery-api/overview.md)|Retrieve optimized and personalized content from Target for delivery to an end user.|[Target Delivery API Postman Collection](/help/dev/before-implement/delivery-api-overview/getting-started.md#postman)||
|[Reporting](../administer/admin-api/admin-api-overview-new.md)|Export activity results and other reporting results.|Reporting APIs are included within the [Target Admin API Postman collection](https://developers.adobetarget.com/api/#admin-postman-collection).||
|[Models](../administer/models-api/models-api-overview.md)|Manage the list of features you want Target to exclude from its machine-learning models (the "blocklist"). The Models API is a type of Admin API, but it is listed here separately due to its unique operations against objects (blocklists) not accessible through the UI.|||

## API Differences

There are important distinctions between Target Admin APIs (including the Recommendations APIs) and Target Delivery APIs:

* Admin APIs let you configure various aspects of Target that you can also configure in the Target UI. The exception to this is the Models API, which lets you configure aspects of Target not available in the UI. Regardless, **all Admin APIs require authentication.**

* Delivery APIs let you retrieve content. Delivery APIs do not require authentication.

To use Target Admin APIs, you must configure authentication using the [Adobe Developer Console](https://developer.adobe.com/console/home). For more information, see [How to Configure Authentication](../before-administer/configure-authentication.md).
