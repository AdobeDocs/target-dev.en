---
title: What is the Adobe Recommendations API?
description: This guide walks developers through hands-on practice using the Adobe Target Recommendations APIs to configure and manage Recommendations catalogs and custom criteria, as well as using the Delivery API to retrieve recommendations content.
feature: APIs/SDKs, Recommendations, Administration & Configuration, Overview
kt: 3815
thumbnail: 
author: Judy Kim
exl-id: 0d03c650-0b00-44b8-a794-10e5d738e42c
TQID: 'https://experienceleague.adobe.com/-bWsxWNZK7LXp0VvKZmsZc68jXcit57v7Wki9hR3wH4'
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: a19e8738-9679-599a-b83b-5f2f15f8e4d6
    internal-label: APIs/SDKs
  - id: dfc8a233-f2b5-4811-bf63-b4262aebc5a5
    internal-label: Administration and configuration
  - id: f69bc5f1-ebdb-4306-a281-f2e77daf734c
    internal-label: Activities and tests
subfeature_v2:
  - id: ed58f4a1-16eb-4c8c-b505-be9da766a9ec
    internal-label: Recommendations
  - id: fc9c2184-9102-403f-bd6c-0055021e4bea
    internal-label: Overview
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
---
# Adobe Recommendations API overview

APIs relevant for Recommendations include [Admin APIs](../../before-administer/target-api-overview.md) that allow you to:

* Manage your catalog of recommendable products or content
* Manage your Recommendations algorithms and activities

Using the Target [Delivery API](../../implement/delivery-api/overview.md) with Recommendations, you can also:

* Retrieve recommendations in JSON, HTML, or XML objects so they can be displayed in web, mobile, email, Internet of Things (IOT), and other channels.

## Description

This guide regarding the Recommendations APIs walk developers through hands-on practice using the Recommendations APIs to configure and manage Recommendations catalogs and custom criteria, as well as using the Delivery API to retrieve recommendations content. By the end, you will be able to:

* Configure and manage entities using the Recommendations API
* Configure and manage custom criteria using the Recommendations API
* Understand how to use Recommendations with the Delivery API to use recommendations results in non-HTML devices

## Audience

This guide is intended for developers new to Target APIs or Recommendations APIs.

## Prerequisites {#prerequisites}

The Target admin APIs require [Adobe authentication setup](../configure-authentication.md). Make sure you have this configured prior to using the Recommendations API.

## Resources

Note the following resources, which are necessary to understand this guide and follow it successfully:

|Resource|Details|
| --- | --- |
|Postman|Get the [Postman app](https://www.postman.com/downloads/) for your operating system. Postman basic is free with account creation. While not required in order to use Adobe Target APIs in general, Postman makes API workflows easier, and Adobe Target provides several Postman collections to help execute its APIs and learn how they operate. The rest of this guide assumes working knowledge of Postman. For assistance, please reference the [Postman documentation](https://learning.getpostman.com/).  |
|References|Familiarity with the following resources is assumed throughout the rest of this guide:<UL><li>[Adobe I/O Github](https://github.com/adobeio)</li><li>[Target Admin and Profile API documentation](../../administer/admin-api/admin-api-overview-new.md)</li><li>[Recommendations API documentation](https://developer.adobe.com/target/administer/recommendations-api/)</li></UL>|
