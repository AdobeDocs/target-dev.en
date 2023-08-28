---
title: Use [!UICONTROL getOffers()] in [!DNL Adobe Target] when using the Node.js SDK
description: Learn how to use [!UICONTROL getOffers()] to execute a decision and retrieve an experience from [!DNL Adobe Target].
feature: APIs/SDKs
exl-id: 3c4125ea-68d4-405e-9b9a-5fa832743153
---
# [!UICONTROL Get Offers] (Node.js)

## Description

`[!UICONTROL getOffers()]` is used to execute a decision and retrieve an experience from [!DNL Adobe Target].


## Method

### getOffers

```js {line-numbers="true"}
TargetClient.getOffers(options: Object): Promise
```

## Parameters

The `options` object has the following structure:

|Name|Type|Required|Default|Description|
| --- |--- | --- | --- | --- |
|Request|Object|Yes|None|Conforms to the [[!DNL Target] Delivery API](/help/dev/implement/delivery-api/overview.md) request|
|visitorCookie|String|No|None|ECID (VisitorId) cookie|
|targetCookie|String|No|None|[!DNL Target] cookie |
|targetLocationHint|String|No|None|[!DNL Target] location hint|
|consumerId|Sting|No|None|consumerIds for [!UICONTROL Analytics for Target] (A4T) stitching|
|CustomerIds|Array|No|None|Customer IDs in VisitorId-compatible format|
|sessionId|String|No|None|Used for linking multiple [!DNL Target] requests|
|visitor|Object|No|new VisitorId|Supply an external VisitorId instance|

## Promise

`Promise` returned has the following structure:

|Name|Type|Description|
| --- | --- | --- |
|request|Object|[[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) request|
|response|Object|[[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) response|
|visitorState|Object|Object that should be passed to Visitor API `getInstance()`|
|targetCookie|Object|[!DNL Target] cookie|
|targetLocationHintCookie|Object|[!DNL Target] location hint cookie|
|analyticsDetails|Array|Analytics payload, in case of client-side Analytics usage|
|responseTokens|Array|A list of [Response tokens](https://experienceleague.adobe.com/docs/target/using/administer/response-tokens.html?).|
|trace|Array|Aggregated trace data for all request mboxes/views|
|status|Object|An object containing the status of the response.|
|decisioningMethod|String|Determines which decisioning method to use ([on-device](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md), server-side, hybrid)|

`targetCookie` and `targetLocationHintCookie` objects used for passing data back to the browser have the following structure:

|Name|Type|Description|
| --- | --- | --- |
|name|String|Cookie name|
|value|Any|Cookie value, the will be converted to string|
|maxAge|Number|The `maxAge` option is a convenience for setting expires relative to the current time in seconds|

The `status` object used for indicating the status of the target response has the following structure:

|Name|Type|Description|
| --- | --- | --- |
|status|Number|HTTP status code|
|message|String|A message about the response. For instance, it may indicate if the response was decided [on-device](/help/dev/implement/server-side/sdk-guides/on-device-decisioning/overview.md) or server-side|
|remoteMboxes|Array|When decisioning Method is `on-device`, an array of mbox names that could not be fully decided on-device is given. In other words, a [[!UICONTROL Target Delivery API]](/help/dev/implement/delivery-api/overview.md) request is needed.|

## Example

### Node.js

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

const request = {
    context: {channel: "web"},
    execute: {
        mboxes: [{
            name: "a1-serverside-ab",
            index: 1
        }]
}};

const response = await targetClient.getOffers({ request });
```
