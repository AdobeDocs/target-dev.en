---
title: Recommendations implementation pattern using at.js
description: Understand how to use the implementation pattern for Recommendations with at.js
feature: APIs/SDKs
level: Experienced
role: Developer
---
# [!DNL Recommendations] implementation pattern using at.js overview

This implementation pattern helps you understand and create your [!DNL Adobe Target Recommendations] implementation when using the [at.js JavaScript library](/help/dev/implement/client-side/atjs/how-atjs-works/overview.md).

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

