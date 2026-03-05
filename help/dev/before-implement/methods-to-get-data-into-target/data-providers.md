---
keywords: implement, implementing, setting up, setup, data providers
description: Get data into [!DNL Target] using data providers.
title: How Do I Get Data into [!DNL Target] Using Data Providers?
feature: Implementation
exl-id: 9971bd96-f736-4965-afe2-b4901c12d006
TQID: https://experienceleague.adobe.com/e8uMaGcACjHiaIT4WSlbKry82mhLHUDTSKmCuuhoWgw
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
  - id: fd0ff162-b6d3-4a11-8aeb-e165a01c0f0a
    internal-label: at.js
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
---
# Data providers

Data providers are a capability that allows you to easily pass data from third parties to [!DNL Adobe Target].

>[!NOTE]
>
>Data providers require at.js 1.3 or later.

## Format

The `window.targetGlobalSettings.dataProviders` setting is an array of data providers.

For more information about the structure for each data provider, see [Data Providers](../../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers).

## Example use cases

Collect data from a third party, such as a weather service, a DMP, or even your own web service. You can then use this data to build audiences, target content, and enrich the visitor profile.

## Benefits of method

This setting lets customers gather data from third-party data providers, such as Demandbase, BlueKai, and custom services, and pass the data to [!DNL Target] as mbox parameters in the global mbox request.

It supports the collection of data from multiple providers via async and sync requests.

Using this approach makes it easy to manage flicker of default page content, while including independent timeouts for each provider to limit the impact on page performance

## Caveats

If the data providers added to `window.targetGlobalSettings.dataProviders` are async, they are executed in parallel. The Visitor API request is executed in parallel with functions added to `window.targetGlobalSettings.dataProviders` to allow a minimum wait time.

at.js does not try to cache the data. If the data provider fetches data only once, the data provider should make sure that data is cached and, when the provider function is invoked, serve the cache data for the second invocation.

## Code examples

Several examples can be found in [Data Providers](../../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers).

## Links to relevant information

Documentation: [Data Providers](../../implement/client-side/atjs/atjs-functions/targetglobalsettings.md#data-providers)

## Training videos:

* [Using Data Providers in Adobe Target](https://experienceleague.adobe.com/docs/target-learn/tutorials/integrations/use-data-providers-to-integrate-third-party-data.html)
* [Implement Data Providers in Adobe Target](https://experienceleague.adobe.com/docs/target-learn/tutorials/integrations/implement-data-providers-to-integrate-third-party-data.html)
