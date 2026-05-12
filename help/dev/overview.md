---
keywords: target developer guide; overview;home
title: Adobe Target Developer Guide
description: How do I implement and administer [!DNL Adobe Target] and work with its APIs and SDKs?
contributors: https://github.com/icaraps
feature: APIs/SDKs
exl-id: 655cff9b-fc04-45cf-9068-5c6c32b70d79
TQID: https://experienceleague.adobe.com/lTn4veG9PKL-ZXohH3qv1UH7lpyLfn80nwuxgehXSy0
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
    internal-label: Audiences
  - id: b050e0cd-2ddd-42cd-a71b-5d9e1fdf75e0
    internal-label: APIs and SDKs
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
    internal-label: Implementation
  - id: dfc8a233-f2b5-4811-bf63-b4262aebc5a5
    internal-label: Administration and configuration
subfeature_v2:
  - id: a94ced60-8199-4549-b453-ede2acb4101e
    internal-label: Hybrid implementation
  - id: c011fe9c-b94b-4a88-93d8-f2acece55112
    internal-label: Administration
  - id: c5abb976-5170-45d6-bcac-66d15d10a4d4
    internal-label: Release notes
  - id: cd7b6938-5837-4ee0-9790-5840997133d9
    internal-label: User management
  - id: e22d67ea-317b-44f8-abd1-52e07f636ca8
    internal-label: Reporting
  - id: fc9c2184-9102-403f-bd6c-0055021e4bea
    internal-label: Overview
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
  - id: d3cdead0-685a-4489-9250-4bb709942f66
    internal-label: Data collection
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
    internal-label: Machine learning
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
---
# [!DNL Adobe Target] Developer Guide

**([View [!DNL Target] documentation updates](https://experienceleague.adobe.com/docs/target/using/release-notes/doc-change.html){target=_blank})**

This *[!DNL Adobe Target] Developer Guide* provides resources and guides for [!DNL Target] developers, including API and SDK documentation to implement and administer [!DNL Target].

>[!NOTE]
>
>In addition to this guide, the following [!DNL Adobe Target] guides are also available:
>
>* [*[!DNL Adobe Target] Business Practitioner Guide*](https://experienceleague.adobe.com/docs/target/using/target-home.html){target=_blank}
>
>* [*[!DNL Adobe Target] Tutorials*](https://experienceleague.adobe.com/docs/target-learn/tutorials/overview.html){target=_blank}
>
>For release information, see [Target release notes (current)](https://experienceleague.adobe.com/docs/target/using/release-notes/release-notes.html){target=_blank} in the *[!DNL Adobe Target] Business Practitioner Guide*.

## Getting started with implementation

**[Before you implement](/help/dev/before-implement/considerations-before-you-implement-target.md)**: Considerations you should address before you implement [!DNL Adobe Target].

## Client-Side implementation

[**Adobe Experience Platform Web SDK**](/help/dev/implement/client-side/aep-web-sdk/aep-web-sdk-overview.md): The [!DNL Adobe Experience Platform Web SDK] lets you interact with the various services in the [!DNL Experience Cloud] (including [!DNL Target]) through the [!UICONTROL Adobe Experience Edge Network].

[**Target at.js JavaScript library**](/help/dev/implement/client-side/overview.md): The at.js JavaScript library improves page load times for web implementations, improves security, and provides better implementation options for single-page applications. 

## Server-Side implementation

[**Target SDK overview**](implement/server-side/server-side-overview.md): Get started with [!DNL Adobe Target] SDKs, including On-device decisioning.

[**Node.js SDK**](implement/server-side/node-js/overview.md): How to use the [!DNL Target] Node.js SDK.

[**Java SDK**](implement/server-side/java/overview.md): How to use the [!DNL Target] Java SDK.

[**.NET SDK**](implement/server-side/net/overview.md): How to use the [!DNL Target] .NET SDK.

[**Python SDK**](implement/server-side/python/overview.md): How to use the [!DNL Target] Python SDK.

## Hybrid implementation

[**Hybrid deployment**](implement/hybrid/hybrid-overview.md): Implement [!DNL Target] using a combination of client-side and server-side implementation.

## Recommendations implementation

[**Recommendations implementation**](implement/recommendations/recommendations.md): Plan and implement [!DNL Adobe Target Recommendations].

## Mobile App implementation

[**AEP Mobile SDK overview**](implement/mobile/overview.md): Overview of how to implement [!DNL Adobe Target] with [!DNL Adobe Experience Platform] Mobile SDKs.

[**AEP Mobile SDK reference**](https://developer.adobe.com/client-sdks/documentation/): Implement [!DNL Adobe Target] with [!DNL Adobe Experience Platform] Mobile SDKs.

## Email implementation

[**Email overview**](implement/email/overview.md): Overview of how to implement [!DNL Adobe Target] in emails.

## API guides

[**Introduction**](before-administer/target-api-overview.md): Overview of [!DNL Adobe Target] APIs.

[**[!DNL Target Delivery API]**](/help/dev/implement/delivery-api/overview.md): Use the [!DNL Adobe Target] Delivery APIs to deliver experiences across web and mobile channels as well as non-browser based IoT devices such as a connected TV, kiosk, or in-store digital screen.

[**[!DNL Target Admin API]**](administer/admin-api/admin-api-overview-new.md): Use the [!DNL Adobe Target] Admin API to manage properties, activities, audiences, offers, properties, reports, mboxes, hosts, environments, and more.

[**[!DNL Target Profile API]**](/help/dev/administer/profile-api/profiles-api.md): Retrieve [!DNL Adobe Target] user profile information.

[**[!DNL Target Reporting API]**](https://developer.adobe.com/target/administer/admin-api/#tag/Reports): Retrieve [!UICONTROL A/B Test] and [!UICONTROL Automated Personalization] activity report data.

[**[!DNL Target Recommendations API]**](https://developer.adobe.com/target/administer/recommendations-api/): Use the [!DNL Target Recommendations] API.

[**[!DNL Target Models API]**](administer/models-api/models-api-overview.md): Manage blocklists to define the features used in [!DNL Target] machine learning models.

[**Admin Console APIs**](https://developer.adobe.com/umapi/): Manage users and product entitlements through the Adobe User Management and User Sync APIs.

[**[!DNL Adobe Experience Platform Edge Network Server API]**](https://experienceleague.adobe.com/docs/experience-platform/edge-network-server-api/overview.html): Use the [!DNL Adobe Experience Platform Edge Network Server] API for a variety of data collection, personalization, advertising, and marketing use cases.

## Resources

* [Adobe open source repo](https://github.com/adobe)
* [Target Node JS SDK Source](https://github.com/adobe/target-nodejs-sdk)
* [Target Node JS SDK Examples Repo](https://github.com/adobe/target-nodejs-sdk-samples)
* [Target Java SDK Source](https://github.com/adobe/target-java-sdk)
* [Target Java SDK Example Repo](https://github.com/adobe/target-java-sdk-samples)
* [Target Implementation](./before-implement/prepare-to-implement-target.md)
* [Target Administration](./before-administer/target-api-overview.md)
* [Adobe Target Dev Docs GitHub Repo](https://github.com/AdobeDocs/target-developers)
* [Adobe Target Release Notes](https://experienceleague.adobe.com/docs/target/using/release-notes/release-notes.html)
* [Adobe Target Business User Guide](https://experienceleague.adobe.com/docs/target/using/target-home.html)

