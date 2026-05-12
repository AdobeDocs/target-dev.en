---
title: Subscribe to events in the [!DNL Adobe Target] .NET SDK
description: Learn how to subscribe to various events that occur within the .NET SDK using the [!UICONTROL OnDeviceDecisioningHandler] object.
feature: APIs/SDKs
exl-id: 7578033f-3de5-4d13-9739-46ad1269ec5f
TQID: https://experienceleague.adobe.com/oeGknU-pW1-XjVrxn8JNEPoFBF8Gntt-vaVnqjdyTC8
product_v2:
  - id: e43347a8-f2c5-4aa4-8623-6f13875d7e3a
    internal-label: Target
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
---
# SDK Events (.NET)

## Description

When [initializing the SDK](initialize-sdk.md), an optional `OnDeviceDecisioningReady` delegate can be provided on the `TargetClientConfig` object, which will be invoked when the SDK is ready for on-device method calls. There are also a couple other delegates available for handling the [!UICONTROL on-device decisioning] artifact download.

## Events

The following delegates can be configured for certain events:

|Name|Arguments|Description|
| --- | --- | --- |
|OnDeviceDecisioningReady|None|Called only once the first time the client is ready for [!UICONTROL on-device decisioning]|
|ArtifactDownloadSucceeded|string contents of artifact file|Called every time an [!UICONTROL on-device decisioning] artifact is downloaded|
|ArtifactDownloadFailed|Exception|Called every time there is a failure to download an [!UICONTROL on-device decisioning] artifact|

## Example

### \.NET

```dotnet {line-numbers="true"}
var clientConfig = new TargetClientConfig.Builder("acmeclient", "1234567890@AdobeOrg")
    .SetDecisioningMethod(DecisioningMethod.OnDevice)
    .SetOnDeviceDecisioningReady(DecisioningReady)
    .SetArtifactDownloadSucceeded(artifact => Console.WriteLine("The artifact was successfully downloaded. Contents: " + artifact))
    .SetArtifactDownloadFailed(exception => Console.WriteLine("The artifact failed to download. Exception: " + exception.Message))
    .Build();

var targetClient = TargetClient.Create(clientConfig);

// ...

static void DecisioningReady()
{
    var mboxRequests = new List<MboxRequest> { new (index: 1, name: "a1-serverside-ab") };

    var targetDeliveryRequest = new TargetDeliveryRequest.Builder()
        .SetExecute(new ExecuteRequest(mboxes: mboxRequests))
        .Build();

    var targetResponse = targetClient.GetOffers(targetDeliveryRequest);
}
```
