---
title: Integration with Experience Cloud A4T Reporting
description: Integration with Experience Cloud, A4T Reporting, Analytics for Target integration
keywords: delivery api, server-side, serverside, integration, a4t
exl-id: 0d09d7a1-528d-4e6a-bc6c-f7ccd61f5b75
feature: Implement Server-side
---
# [!UICONTROL Analytics for Target] (A4T) reporting

[!DNL Adobe Target] supports A4T reporting for both on-device decisioning and server-side [!DNL Target] activities. There are two configuration options for enabling A4T reporting:

* [!DNL Adobe Target] automatically forwards the analytics payload to [!DNL Adobe Analytics], or
* The user requests the analytics payload from [!DNL Adobe Target]. ([!DNL Adobe Target] returns the [!DNL Adobe Analytics] payload back to the caller.)

>[!NOTE]
>
>On-device decisioning only supports A4T reporting of which [!DNL Adobe Target] automatically forwards the analytics payload to [!DNL Adobe Analytics]. Retrieving the analytics payload from [!DNL Adobe Target] is not supported.

## Pre-requisites

1. Configure the activity in the [!DNL Adobe Target] UI with [!DNL Adobe Analytics] as the reporting source, and ensure the accounts are enabled for A4T.
1. The API user generates the Adobe [!UICONTROL Marketing Cloud Visitor ID] and ensures this ID is available when the [!DNL Target] request is executed.

## [!DNL Adobe Target] automatically forwards the [!DNL Analytics] payload

[!DNL Adobe Target] can automatically forward the analytics payload to [!DNL Adobe Analytics] if the following identifiers are provided:

1. `supplementalDataId`: The ID that is utilized to stitch between [!DNL Adobe Analytics] and [!DNL Adobe Target]. In order for [!DNL Adobe Target] and [!DNL Adobe Analytics] to correctly stitch data together, the same `supplementalDataId` needs to be passed to both [!DNL Adobe Target] and [!DNL Adobe Analytics].
1. `trackingServer`: The [!DNL Adobe Analytics] Server.

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");

const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};

const targetClient = TargetClient.create(CONFIG);

targetClient.getOffers({
  request: {     
    id: {
      marketingCloudVisitorId : "2304820394812039",
      tntId: "d359234570e044f14e1faeeba02d6ab23439914e.35_0",
      thirdPartyId:"23423432"
    },
    experienceCloud: {
      analytics: {
        logging: "server_side",
        supplementalDataId: "7D3AA246CC99FD7F-1B3DD2E75595498E",
        trackingServer: "jimsbrims.sc.omtrds.net"
      }
    }, 
    execute: {
      mboxes: [{
        name: "some-mbox"
      }]
    }       
  }
})
.then(console.log)
.catch(console.error);
```

>[!TAB Java]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

VisitorId id = new VisitorId()
  .tntId("d359234570e044f14e1faeeba02d6ab23439914e.35_0")
  .thirdPartyId("B234A029348")
  .marketingCloudVisitorId("10527837386392355901041112038610706884");
Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

AnalyticsRequest analyticsRequest =
    new AnalyticsRequest()
        .trackingServer("jimsbrims.sc.omtrds.net")
        .logging(LoggingType.SERVER_SIDE)
        .supplementalDataId("7D3AA246CC99FD7F-1B3DD2E75595498E");
ExperienceCloud expCloud =
    new ExperienceCloud()
        .setAnalytics(analyticsRequest);

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .experienceCloud(expCloud)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

## User retrieves analytics payload from [!DNL Adobe Target]

A user can retrieve the [!DNL Adobe Analytics] payload for a given mbox, then send it to [!DNL Adobe Analytics] via the [Data Insertion API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md). When an [!DNL Adobe Target] request is fired, pass `client_side` to the `logging` field in the request. This request returns a payload if the specified mbox is present in an activity that is using [!DNL Analytics] as the reporting source.

>[!BEGINTABS]

>[!TAB Node.js]

```js {line-numbers="true"}
const TargetClient = require("@adobe/target-nodejs-sdk");
const CONFIG = {
  client: "acmeclient",
  organizationId: "1234567890@AdobeOrg"
};
const targetClient = TargetClient.create(CONFIG);
targetClient.getOffers({
  request: {     
    id: {
      marketingCloudVisitorId : "2304820394812039",
      tntId: "d359234570e044f14e1faeeba02d6ab23439914e.35_0",
      thirdPartyId:"23423432"
    },
    experienceCloud: {
      analytics: {
        logging: "client_side"
      }
    },  
    execute: {
      mboxes: [{
        name: "some-mbox"
      }]
    }       
  }
})
.then(console.log)
.catch(console.error);
```

>[!TAB Java]

```java {line-numbers="true"}
ClientConfig config = ClientConfig.builder()
  .client("acmeclient")
  .organizationId("1234567890@AdobeOrg")
  .build();
TargetClient targetClient = TargetClient.create(config);

VisitorId id = new VisitorId()
  .tntId("d359234570e044f14e1faeeba02d6ab23439914e.35_0")
  .thirdPartyId("B234A029348")
  .marketingCloudVisitorId("10527837386392355901041112038610706884");
Context context = new Context().channel(ChannelType.WEB);
MboxRequest mbox = new MboxRequest()
  .name("some-mbox")
  .index(0);
ExecuteRequest executeRequest = new ExecuteRequest()
  .mboxes(Arrays.asList(mbox));

AnalyticsRequest analyticsRequest =
    new AnalyticsRequest()
        .logging(LoggingType.CLIENT_SIDE);
ExperienceCloud expCloud =
    new ExperienceCloud()
        .setAnalytics(analyticsRequest);

TargetDeliveryRequest request = TargetDeliveryRequest.builder()
  .context(context)
  .execute(executeRequest)
  .experienceCloud(expCloud)
  .build();

TargetDeliveryResponse offers = targetClient.getOffers(request);
```

>[!ENDTABS]

Once you have specified `logging = client_side`, you will receive the payload in the mbox field.

If the response from [!DNL Target] contains anything in the `analytics -> payload` property, forward it as it is to [!DNL Adobe Analytics]. [!DNL Adobe Analytics] knows how to process this payload. This can be done in a GET request using the following format:

```
https://{datacollectionhost.sc.omtrdc.net}/b/ss/{rsid}/{content_type_num}/{code_ver}/{session}?pe=tnt&tnta={payload}&c.&a.&target.&sessionId={sessionId}&.target&.a&.c&mid={mid}
```

### Query string parameters and variables

|Field Name|Required|Description|
| --- | --- | --- |
|`rsid`|Yes|The report suite ID|
|`content_type_num`|Yes|Always set to "0"|
|`code_ver`|Yes|Always set to "MOBILE-1.0"|
|`session`|Yes|Always set to "0"|
|`pe`|Yes|Page event. Always set to `tnt`|
|`tnta`|Yes|[!DNL Analytics] payload returned by [!DNL Target] server in `analytics -> payload -> tnta`|
|`sessionId`|Yes|[!DNL Target] session Id of the ongoing session|
|`mid`|Yes|Marketing Cloud Visitor ID|

### Required header values

|Header Name|Header Value|
| --- | --- |
|Host|Analytics data collection server (eg: `adobeags421.sc.omtrdc.net`)|

### Sample A4T data insertion HTTP Get call

Non-URL-encoded version For Readability (format not to be used for API calls):

```
https://demo.sc.omtrdc.net/b/ss/myCustomRsid/0/MOBILE-1.0/0?tnta=253236:0:0|0,253236:0:0|2,253236:0:0|1,253613:0:0|0,253613:0:0|2,253613:0:0|1&c.&a.&target.&sessionId=45c08980-f4b9-4e11-96db-067d58e49f74&.target&.a&.c&pe=tnt&mid=69170113867710665996968872592584719577
```

URL-encoded version (format to be used for API calls):

```
https://demo.sc.omtrdc.net/b/ss/myCustomRsid/0/MOBILE-1.0/0?tnta=253236%3A0%3A0%7C0%2C253236%3A0%3A0%7C2%2C253236%3A0%3A0%7C1%2C253613%3A0%3A0%7C0%2C253613%3A0%3A0%7C2%2C253613%3A0%3A0%7C1&c.%26a.%26target.%26sessionId=45c08980-f4b9-4e11-96db-067d58e49f74%26.target%26.a%26.c&pe=tnt&mid=69170113867710665996968872592584719577 
```