---
title: Use getAttributes in [!DNL Adobe Target] with the .NET SDK
description: Learn how to use getAttributes() to fetch experimentation and personalized experiences from [!DNL Target] and extract attribute values.
feature: APIs/SDKs
exl-id: 808da83d-3077-468b-a2ad-e35c25905f7d
TQID: https://experienceleague.adobe.com/aflHPozCwJ-6fB7X-2jLaBvs42Ohz6OzwZ7AvkahCE8
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: bcc5edb5-84c3-4940-9f84-ed88b6c16274
    internal-label: Experimentation
---
# Get Attributes (.NET)

## Description

`GetAttributes()` is used to fetch experimentation and personalized experiences from [!DNL Target] and extract attribute values.

## Method

### getAttributes

```dotnet {line-numbers="true"}
TargetAttributes TargetClient.GetAttributes(TargetDeliveryRequest targetRequest, params string[] mboxes)
```

## Parameters

|Name|Type|Required|Default|Description|
| --- | --- | --- | --- | --- |
|targetRequest|TargetDeliveryRequest|No|null|The same [!DNL Target] request as used for [Get Offers​](get-offers.md)|
|mboxNames|params string[]|No|null|A parameter array of mbox names|

## Result

A `TargetAttributes` object is returned from `TargetClient.GetAttributes()` which has the following properties and methods:

|Property/Method|Return Type|Description|
| --- | --- | --- |
|Response|TargetDeliveryResponse|Returns the response object normally returned by [Get Offers](get-offers.md)|
|ToDictionary|IReadOnlyDictionary|Returns a dictionary of dictionaries with key value pairs grouped by mbox names|
|ToMboxDictionary(mboxName)|IReadOnlyDictionary|Returns a dictionary with key value pairs for the provided mbox|
|GetBoolean(mboxName, key, defaultValue)|bool|Returns the value for a specified mbox name and attribute key|
|GetString(mboxName, key, defaultValue)|string|Returns the value for a specified mbox name and attribute key|
|GetInteger(mboxName, key, defaultValue)|int|Returns the value for a specified mbox name and attribute key|
|GetDouble(mboxName, key, defaultValue)|double|Returns the value for a specified mbox name and attribute key|
|GetValue(mboxName, key, defaultValue)|T|Returns the value for a specified mbox name and attribute key|

## Example

### \.NET

```dotnet {line-numbers="true"}
var targetClientConfig = new TargetClientConfig.Builder("acmeClient", "ABCDEF012345677890ABCDEF0@AdobeOrg")
    .Build();

var targetClient = TargetClient.Create(targetClientConfig);

var mboxRequests = new List<MboxRequest> { new (index: 1, name: "a1-serverside-ab") };

var targetDeliveryRequest = new TargetDeliveryRequest.Builder()
    .Build();

var offerAttributes = targetClient.GetAttributes(targetDeliveryRequest, "demo-engineering-flags");

//returns just the value of searchProviderId from the mbox offer
var searchProviderId = offerAttributes.GetString("demo-engineering-flags", "searchProviderId");

//returns a simple Dictionary representing the mbox offer
var engineeringFlags = offerAttributes.ToMboxDictionary("demo-engineering-flags");

//  the value of engineeringFlags looks like this
//  {
//      "cdnHostname": "cdn.cloud.corp.net",
//      "searchProviderId": 143,
//      "hasLegacyAccess": false
//  }

var assetUrl = $"http://{engineeringFlags["cdnHostname"]}/path/to/asset";
```
