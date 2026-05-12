---
title: Initialize the Node.js SDK using the create method
description: Learn how to use the create method to initialize the Node.js SDK and instantiate the [!DNL Target] client to make calls to [!DNL Adobe Target] for experiments and personalized experiences.
feature: APIs/SDKs
exl-id: 71516e44-508a-4d8d-9f2b-7c54243e9c60
TQID: https://experienceleague.adobe.com/uawle0-l5bcv-FuXMLkPc8kIf8DvbkRqAYelr-ehNLk
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
feature_v2:
  - id: c93393a4-e558-47e1-992e-c91ed4d480ce
    internal-label: Implementation
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
---
# Initialize the Node.js SDK

## Description

Use the `create` method in order to initialize the Node.js SDK and instantiate the [!UICONTROL Target] client to make calls to [!DNL Adobe Target] for experiments and personalized experiences.

## Method

**create**

```js {line-numbers="true"}
TargetClient.create(options: Object): TargetClient
```

## Parameters

`options` has the following structure:

|Name|Type|Required|Default|Description|
| --- | --- | --- | --- | --- |
|client|String|Yes|None|[!UICONTROL Adobe Target Client ID]|
|organizationId|String|Yes|None|[!UICONTROL Experience Cloud Organization ID]|
|environment|String|No|production|Target environment name. In the [!DNL Target] UI, [!UICONTROL Administration] > [!UICONTROL Environments].|
|timeout|Number|No|3000|Timeout in milliseconds|
|serverDomain|String|No|`*client*.tt.omtrdc.net`|Overrides default hostname|
|secure|Boolean|No|true|Unset to enforce HTTP scheme|
|logger|Object|No|NOOP logger|Replaces the default NOOP logger|
|targetLocationHint|String|No|None|Target location hint|
|fetchApi|Function|No|global.fetch or window.fetch|[fetch](https://fetch.spec.whatwg.org/) is used by the SDK for http requests. By default node-fetch or the browser implementation of fetch is used. But an alternative implementation can be provided using `fetchApi`|
|propertyToken|String|No|None|**Target Property Token**. If specified here, all `getOffers` calls will use this value. **For on-device decisioning**, the SDK will only download the artifact that contains the qualified activities for the property token set in `propertyToken`|
|decisioningMethod|String|No|server-side|Determines which decisioning method to use ([on-device](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md), server-side, hybrid)|
|pollingInterval|Number|No|300000 (5 minutes)|Polling interval for the [on-device decisioning rule artifact](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md) (in milliseconds)|
|artifactLocation|String|No|None|A fully qualified url to the [on-device decisioning rule artifact](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md). Overrides internally determined location.|
|artifactPayload|Object|No|None|The JSON payload of the [on-device decisioning rule artifact](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/rule-artifact-overview.md). If specified, it is used instead of requesting one from a URL.|
|[events](sdk-events.md)|Object<String,Function>|No|None|An optional object with event name keys and callback function values|
|telemetryEnabled|Boolean|No|true|When enabled, Adobe will collect SDK feature usage and performance telemetry data. Personal data is not collected.|

## Example

### Node.js

```js {line-numbers="true"}
const CONFIG = {
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
    events: {clientReady: targetClientReady }
};

const targetClient = TargetClient.create(CONFIG);

function targetClientReady() {
    // make calls to Adobe Target
}
```
