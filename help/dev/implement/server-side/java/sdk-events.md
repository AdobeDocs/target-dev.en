---
title: Subscribe to events in the [!DNL Adobe Target] Java SDK
description: Learn how to subscribe to various events that occur within the Java SDK using the [!UICONTROL OnDeviceDecisioningHandler] object.
feature: APIs/SDKs
role: Developer
---

# SDK Events (Java)

## Description

When [initializing the SDK](initialize-sdk.md), an optional `OnDeviceDecisioningHandler` object can be provided on the `ClientConfig` object. It can be used to subscribe to various events that occur within the SDK. For instance, the `onDeviceDecisioningReady` event may be used with a callback function that will be invoked when the SDK is ready for method calls.

## Events

The `OnDeviceDecisioningHandler` object contains the following callbacks, which are called for certain events:

|Name|Arguments|Description|
| --- | --- | --- |
|onDeviceDecisioningReady|None|Called only once the first time the client is ready for [!UICONTROL on-device decisioning]|
|artifactDownloadSucceeded|byte[] contents of artifact file|Called every time a [!UICONTROL on-device decisioning] artifact is downloaded|
|artifactDownloadFailed|Exception|Called every time there is a failure to download a [!UICONTROL on-device decisioning] artifact|

## Example

### SDK Events

```javascript {line-numbers="true"
ClientConfig clientConfig = ClientConfig.builder()
        .client("acmeclient")
        .organizationId("1234567890@AdobeOrg")
        .defaultDecisioningMethod(DecisioningMethod.ON_DEVICE)
        .onDeviceDecisioningHandler(new OnDeviceDecisioningHandler() {
            @Override
            public void onDeviceDecisioningReady() {
                // make getOffers requests
                makeTargetRequests();
            }

            @Override
            public void artifactDownloadSucceeded(byte[] artifactData) {
                System.out.println("The artifact was successfully downloaded.");
            }

            @Override
            public void artifactDownloadFailed(TargetClientException e) {
                System.out.println("The artifact failed to download.");
            }
        }).build();

TargetClient targetJavaClient = TargetClient.create(clientConfig);


void makeTargetRequests() {
    List<MboxRequest> mboxRequests = new ArrayList<>();
    mboxRequests.add((MboxRequest) new MboxRequest().name("a1-serverside-ab").index(1));

    TargetDeliveryRequest targetDeliveryRequest = TargetDeliveryRequest.builder()
            .context(new Context().channel(ChannelType.WEB))
            .execute(new ExecuteRequest().setMboxes(mboxRequests))
            .build();

    TargetDeliveryResponse targetResponse = targetJavaClient.getOffers(targetDeliveryRequest);
}
```