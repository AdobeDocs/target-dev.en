---
title: How to use asynchronous requests in the [!DNL Adobe Target] Node.js SDK
description: Learn how [!DNL Target] Node.js SDK supports asynchronous requests, which can reduce the effective target time to zero.
feature: APIs/SDKs
exl-id: aa06f3ca-7d2a-4334-8092-730a8705dfb0
---
# Get Attributes (Node.js)

## Description

`[!UICONTROL getAttributes()]` is used to fetch experimentation and personalized experiences from [!DNL Target] and extract attribute values.

## Method

### getAttributes

```js {line-numbers="true"}
TargetClient.getAttributes(mboxNames: Array, options: Object): Promise
```

## Parameters

|Name|Type|Required|Default|
| --- | --- | --- |--- |
|mboxNames|Array|Yes|None|
|options|Object|No|None|

## Promise

The `Promise` returned by `TargetClient.getAttributes()` resolves an object with the following methods:

|Method|Return Type|Description|
| --- | --- | --- |
|getValue(mboxName, key)|Any|Returns the value for a specified mbox name and attribute key|
|asObject(mboxName)|Object|Returns a simple json object with key value pairs|
|getResponse()|[getOffers Response](https://github.com/jasonwaters/target-nodejs-sdk#targetclientgetoffers)|Returns the response object normally returned by `getOffers`|

## Example

### Node.js

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);
const offerAttributes = await targetClient.getAttributes(["demo-engineering-flags"]);


//returns just the value of searchProviderId from the mbox offer
const searchProviderId = offerAttributes.getValue("demo-engineering-flags", "searchProviderId");

//returns a simple JSON object representing the mbox offer
const engineeringFlags = offerAttributes.asObject("demo-engineering-flags");

//  the value of engineeringFlags looks like this
//  {
//      "cdnHostname": "cdn.cloud.corp.net",
//      "searchProviderId": 143,
//      "hasLegacyAccess": false
//  }

const assetUrl = `http://${engineeringFlags.cdnHostname}/path/to/asset`;
```
