---
keywords: at.js integration, supported integrations, unsupported integrations, third party integrations
description: See the integrations supported (and not supported) by [!DNL Adobe Target] at.js, including [!UICONTROL Analytics for Target] (A4T), the [!UICONTROL Experience Cloud ID Service], and more.
title: What Integrations Does at.js Support?
feature: at.js
exl-id: d2c61e77-5fc7-4c35-905b-76b8c4f9df4b
TQID: https://experienceleague.adobe.com/RdcxcIGufo2O5aKPqIAJVINkCzZ1Brcv8EXiX1n4buc
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: adee20bd-51f4-461d-b9db-d215f8756eeb
    internal-label: Audiences
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
    internal-label: Implementation
  - id: f7c7de77-382f-4f48-8b36-61a170f06d3d
    internal-label: Integrations
subfeature_v2:
  - id: df62f171-ac37-440f-8f0f-f41a72ebdd34
    internal-label: Analytics integration
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
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
    internal-label: Customer experience
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
  - id: e6ff21d3-dec6-4298-8590-7c749fffaf78
    internal-label: Content and assets
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
    internal-label: Machine learning
---
# at.js integrations

Information about common integrations with [!DNL Adobe Target] and their support status with at.js.

If you have a compelling need for an integration that is not supported or mentioned here, please contact your account representative or consultant.

## Supported Integrations

| Integration | Details |
|--- |--- |
|[!UICONTROL Analytics for Target] (A4T)|See [Adobe Analytics as the Reporting Source for Adobe Target (A4T)](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/a4t.html).|
|[!UICONTROL Profiles & Audiences] (P&A)|See [Audiences](https://experienceleague.adobe.com/docs/core-services/interface/audiences/audience-library.html) in the *Core Services User Guide*.|
|[!UICONTROL Experience Cloud ID Service]|See the [Adobe Experience Cloud ID Service documentation](https://experienceleague.adobe.com/docs/id-service/using/home.html).|
|[!UICONTROL Tags in Adobe Experience Platform]|[!UICONTROL Tags in Adobe Experience Platform] are the next generation of tag management capabilities from [!DNL Adobe]. [!UICONTROL Tags] give customers a simple way to deploy and manage the analytics, marketing, and advertising tags necessary to power relevant customer experiences. See [Implement [!DNL Target] using Adobe Experience Platform](../how-to-deployatjs/implement-target-using-adobe-launch.md).|
|[!UICONTROL Adobe Experience Manager] (AEM) Cloud Service|The [!UICONTROL AEM Cloud Service] enables the creation of [!UICONTROL A/B Test] and [!UICONTROL Experience Targeting] activities within the AEM workflow. Supports at.js with [!UICONTROL Adobe Experience Manager] 6.2 with FP-11577 (or later). For more information, see [Integrating with [!DNL Adobe Target]](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html) and select your AEM version.|
|[!UICONTROL AEM Experience Fragments]|Experience fragments created in AEM in [!DNL Target] activities let you combine the ease-of-use and power of AEM with powerful Automated Intelligence (AI) and Machine Learning (ML) capabilities in [!DNL Target] to test and personalize experiences at scale.  AEM brings together all of your content and assets in a central location to fuel your personalization strategy. AEM lets you easily create content for desktops, tablets, and mobile devices in one location without writing code. There's no need to create pages for every device—AEM automatically adjusts each experience using your content.  See [AEM experience fragments](https://experienceleague.adobe.com/docs/target/using/experiences/offers/aem-experience-fragments.html).|

## Unsupported Integrations

| Integration | Details |
|--- |--- |
|Legacy [!DNL Target] to [!DNL SiteCatalyst] Integration|This was the integration that sent campaign and recipe ids to [!DNL SiteCatalyst] via the page call so you could do reporting in the [!DNL SiteCatalyst] UI. This functionality is replaced by A4T.|
|Legacy [!DNL Target] to [!DNL SiteCatalyst] Integration|This was the integration that made mbox calls named `"SiteCatalyst: Event"` and `"SiteCatalyst: Purchase"` so you could build success metrics and user profiles based on evars and props. This functionality is replaced by A4T and P&A.|
|Legacy [!DNL Audience Manager] (AAM) to [!DNL Target] Integration|This was the integration that made a front-end API call to retrieve AAM segments and then sent them as mbox parameters on every mbox call on the page.|

## Third-Party Integrations

| Integration | Details |
|--- |--- |
|Other Tag Managers|at.js should work with non-Adobe tag management platforms, but be careful using custom integration features that other vendors have developed. Their integrations might be dependent on internal  mbox.js functions that no longer exist in  at.js.|
|Third-party data providers (e.g. Demandbase, Bluekai, weather APIs)|Many third-party data providers used to supplement Target's user profiling can be integrated using the at.js [Data Providers](../atjs-functions/targetglobalsettings.md#data-providers) feature.|
