---
title: Subscribe to events in the [!DNL Adobe Target] Node.js SDK
description: Learn how to subscribe to various events that occur within the Node.js SDK using the [!UICONTROL OnDeviceDecisioningHandler] object.
feature: APIs/SDKs
exl-id: 40c53840-a560-4819-ae04-f527c36b22fe
---
# SDK Events (Node.js)

## Description

When [initializing the SDK](initialize-sdk.md), the `options.events` object is an optional object with event name keys and callback function values. It can be used to subscribe to various events that occur within the SDK. For instance the `clientReady` event may be used with a callback function that will be invoked when the SDK is ready for method calls.

When the callback function is called, an event object is passed in. Each event has a `type` corresponding to the event name. Some events include additional properties with pertinent information.

## Events

|Event Name (type)|Description|Additional Event Properties|
| --- | --- | --- |
|clientReady|Emitted when the artifact has downloaded and the SDK is ready for `getOffers` calls. Recommended when using on-device decisioning method.|
|artifactDownloadSucceeded|Emitted each time a new artifact is downloaded.|artifactPayload, artifactLocation|
|artifactDownloadFailed|Emitted each time an artifact fails to download.|artifactLocation, error|

## Example

### Node.js

```js {line-numbers="true"}
const targetClient = TargetClient.create({
    client: "acmeclient",
    organizationId: "1234567890@AdobeOrg",
    decisioningMethod: "on-device",
    events: {
        clientReady: onTargetClientReady,
        artifactDownloadSucceeded: onArtifactDownloadSucceeded,
        artifactDownloadFailed: onArtifactDownloadFailed
    }
});

function onTargetClientReady() {
    // make getOffers requests
    targetClient.getOffers({...})            
}

function onArtifactDownloadSucceeded(event) {
    console.log(`The artifact was successfully downloaded from '${event.artifactLocation}'`);
    // optionally do something with event.artifactPayload, like persist it
}

function onArtifactDownloadFailed(event) {
    console.log(`The artifact failed to download from '${event.artifactLocation}' with the following error message: ${event.error.message}`);
}
```
