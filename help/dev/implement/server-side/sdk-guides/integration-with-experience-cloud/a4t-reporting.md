---
title: Integration with Experience Cloud A4T Reporting
description: Integration with Experience Cloud, A4T Reporting, Analytics for Target integration
keywords: delivery api, server-side, serverside, integration, a4t
exl-id: 0d09d7a1-528d-4e6a-bc6c-f7ccd61f5b75
feature: Implement Server-side
---
# Analytics for Target (A4T) reporting

[!DNL Adobe Target] supports A4T reporting for both on-device decisioning and server-side Target activities. There are two configuration options for enabling A4T reporting:

* [!DNL Adobe Target] automatically forwards the analytics payload to [!DNL Adobe Analytics], or
* The user requests the analytics payload from [!DNL Adobe Target]. ([!DNL Adobe Target] returns the [!DNL Adobe Analytics] payload back to the caller.)

>[!NOTE]
>
>On-device decisioning only supports A4T reporting of which [!DNL Adobe Target] automatically forwards the analytics payload to [!DNL Adobe Analytics]. Retrieving the analytics payload from [!DNL Adobe Target] is not supported.

## Pre-requisites

1. Configure the activity in the [!DNL Adobe Target] UI with [!DNL Adobe Analytics] as the reporting source, and ensure the accounts are enabled for A4T.
1. The API user generates the Adobe Marketing Cloud Visitor ID and ensures this ID is available when the Target request is executed.

## [!DNL Adobe Target] automatically forwards the Analytics payload

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

A user can retrieve the [!DNL Adobe Analytics] payload for a given mbox, then send it to [!DNL Adobe Analytics] via the [Data Insertion API](https://github.com/AdobeDocs/analytics-1.4-apis/blob/master/docs/data-insertion-api/index.md). When an [!DNL Adobe Target] request is fired, pass `client_side` to the `logging` field in the request. This will return a payload if the specified mbox is present in an activity that is using Analytics as the reporting source.

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

If the response from Target contains anything in the `analytics -> payload` property, forward it as it is to [!DNL Adobe Analytics]. [!DNL Adobe Analytics] knows how to process this payload. This can be done in a GET request using the following format:

```
https://{datacollectionhost.sc.omtrdc.net}/b/ss/{rsid}/0/CODEVERSION?pe=tnt&tnta={payload}&mid={mid}&vid={vid}&aid={aid}
```

### Query String Parameters and Variables

|Field Name|Required|Description|
| --- | --- | --- |
|`rsid`|Yes|The report suite ID|
|`pe`|Yes|Page event. Always set to `tnt`|
|`tnta`|Yes|Analytics payload returned by Target server in `analytics -> payload -> tnta`|
|`mid`|Yes|Marketing Cloud Visitor ID|

### Required Header Values

|Header Name|Header Value|
| --- | --- |
|Host|Analytics data collection server (eg: `adobeags421.sc.omtrdc.net`)|

### Sample A4T Data Insertion HTTP Get Call

```
https://demo.sc.omtrdc.net/b/ss/myCustomRsid/0/MOBILE-1.0?pe=tnt&tnta=285408:0:0|2&mid=2304820394812039
```
