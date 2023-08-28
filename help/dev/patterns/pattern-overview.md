---
title: Implementation patterns overview
description: Understand how to use implementation patterns
feature: APIs/SDKs
level: Experienced
role: Developer
hide: yes
hidefromtoc: yes
---
# Implementation patterns overview

[!DNL Adobe Target] implementation patterns help you understand and create the following architecture for your [!DNL Target] implementation.

Click image to expand to full screen.

![Adobe Target architecture diagram](/help/dev/patterns/assets/architecture-chart.png){width="600" zoomable="yes"}

Note that the numbers in the image do not indicate the sequence of operations:

1. Client-side SDKs for [!DNL Adobe Target] and [!DNL Experience Cloud ID Service]
1. [!DNL Target Delivery API] call
1. ECID acquisition call
1. Bulk profile update API and [!DNL Customer Attributes] (CA) service
1. Profile data ingestion from customer's data sources to [!DNL Target] profile store
1. Collecting profile/behavioral data and deciding which experience to show to the end user
1. Experiences render on the page
1. at.js renders the experiences on the page

Each pattern consists of different parts. Each part corresponds to a critical implementation requirement for your [!DNL Target] implementation.

Each part is explained on a separate page in this guide. For example, the [!DNL Target] implementation pattern contains the following pages: 

* Initialize SDK
* Enrich Profile
* Render Experiences
* Notify [!DNL Target]

