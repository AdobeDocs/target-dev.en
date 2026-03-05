---
title: Recommendations implementation pattern using at.js
description: Understand how to use the implementation pattern for Recommendations with at.js
feature: APIs/SDKs
level: Experienced
role: Developer
exl-id: d568cd1d-acc3-42e0-ae2c-5787e6f361f8
TQID: https://experienceleague.adobe.com/uYNa5mL-8ffPS-ddjnQzILnPFMbjNJqKZDmQT8qFeGA
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
    internal-label: Implementation
subfeature_v2:
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
    internal-label: at.js
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
    internal-label: Behavioral data
  - id: d3cdead0-685a-4489-9250-4bb709942f66
    internal-label: Data collection
---
# [!DNL Recommendations] implementation pattern using at.js overview

This implementation pattern helps you understand and create your [!DNL Adobe Target Recommendations] implementation when using the [at.js JavaScript library](/help/dev/implement/client-side/atjs/how-atjs-works/how-atjs-works.md).

Click image to expand to full screen.

![Adobe Target architecture diagram](/help/dev/patterns/assets/architecture-chart.png){width="600" zoomable="yes"}

Note that the numbers in the image do not indicate the sequence of operations:

1. Client-side SDKs for [!DNL Adobe Target] and [!DNL Experience Cloud ID Service]
1. [!DNL Target Delivery API] call
1. [!UICONTROL Experience Cloud ID] (ECID) acquisition call
1. Bulk profile update API and [!DNL Customer Attributes] (CA) service
1. Profile data ingestion from customer's data sources to [!DNL Target] profile store
1. Collecting profile and behavioral data and deciding which experience to show to the visitor
1. Experiences render on the page
1. at.js renders the experiences on the page

Each pattern consists of different parts, with each part corresponding to a critical implementation requirement for your [!DNL Target] implementation.

Each part is explained in a separate article in this guide: 

* [Initialize SDKS](/help/dev/patterns/recs-atjs/initialize-sdk.md)
* [Configure data collection](/help/dev/patterns/recs-atjs/data-collection.md)
* [Render experiences](/help/dev/patterns/recs-atjs/render-experiences.md)
* [Notify Target](/help/dev/patterns/recs-atjs/notify-target.md)
