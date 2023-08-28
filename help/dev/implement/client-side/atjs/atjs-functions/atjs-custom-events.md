---
keywords: custom events, at.js, request failed, request succeeded, content rendering failed, content rendering succeeded, library loaded, request start, content rendering start, content rendering no offers, content rendering redirect, custom events2
description: Use custom events for the [!DNL Adobe Target] at.js JavaScript library to be notified when an mbox request or offer fails or succeeds.
title: How Do I Use at.js Custom Events?
feature: at.js
exl-id: a4baed9a-9eb8-4343-9834-709b03e44ca2
---
# at.js custom events

Information about `at.js custom events`, which lets you know when an mbox request or offer fails or succeeds.

Historically, mbox.js (now deprecated) didn't let other JavaScript code that runs on the page know what happens behind the scenes. With the advancement of at.js, we had a unique opportunity to fix this issue.

According to our customers there are several scenarios that they would like to be notified of, including:

* An mbox request failed due to timeout, wrong status code, JSON parse error, etc. 
* An mbox request succeeded. 
* Offer rendering failed due to wrapping mbox element missing, selector can not be found, etc. 
* Offer rendering succeeded. DOM changes have been applied.

Pre-defined events have a structure that allows you to extract the required data, based on event type.

To make sure that events can be used in different scenarios, the custom events have a payload object that is assigned to the detail property of the event object (that is passed to the handler). Also to avoid passing strings as event names, the events are exposed as constants using `adobe.target.event` namespace.

## Structure

| Key | Type | Description |
|--- |--- |--- |
|type|String|There are several scenarios in which you would like to be notified to help in tracing, debugging, and customizing interaction with at.js.<p>Each custom event listed below has two formats: a "constant" and a "string value."<ul><li>**Constants**: Prepended with `adobe.target.event.`, presented in all caps, and contain underscore characters. To subscribe to custom events *after* at.js loads but *before* the mbox response has been received, use the constant.</li><li>**String Values**: Lowercase and contain dashes. To subscribe to custom events *before* at.js loads, use the string value.</li></ul>**Request Failed**<p>Constant: `adobe.target.event.REQUEST_FAILED`<p>String value: `at-request-failed`<p>Description: An mbox request failed due to timeout, wrong status code, JSON parse error, etc.<p>**Request Succeeded**<p>Constant: `adobe.target.event.REQUEST_SUCCEEDED`<p>String Value: `at-request-succeeded`<p>Description: An mbox request was successful.<p>**Content Rendering Failed**<p>Constant: `adobe.target.event.CONTENT_RENDERING_FAILED`<p>String Value: `at-content-rendering-failed`<p>Description: Offer rendering failed due to wrapping mbox element missing, selector can not be found, etc.<p>**Content Rendering Succeeded**<p>Constant: `adobe.target.event.CONTENT_RENDERING_SUCCEEDED`<p>String Value: `at-content-rendering-succeeded`<p>Description: Offer rendering was successful. DOM changes have been applied.<p>**Library Loaded**<p>Constant: `adobe.target.event.LIBRARY_LOADED`<p>String Value: `at-library-loaded`<p>Description: This event is ideal to track when at.js has been fully loaded. You can use this event to customize global mbox execution. You can also use this event to disable the global mbox and then listen for this event to fire the global mbox later.<p>**Request Start**<p>Constant: `adobe.target.event.REQUEST_START`<p>String Value: `at-request-start`<p>Description: This event is fired before an HTTP request is executed. You can use this event for performance measurements using the Resource Timing API.<p>**Content Rendering Start**<p>Constant: `adobe.target.event.CONTENT_RENDERING_START`<p>String Value: `at-content-rendering-start`<p>Description: This event is fired before selector polling is started and content is rendered to the page. You can use this event to track the content rendering progress.<p>**Content Rendering No Offers**<p>Constant: `adobe.target.event.CONTENT_RENDERING_NO_OFFERS`<p>String Value: `at-content-rendering-no-offers`<p>Description: This event is fired when there are no offers returned.<p>**Content Rendering Redirect**<p>Constant: `adobe.target.event.CONTENT_RENDERING_REDIRECT`<p>String Value: `at-content-rendering-redirect`<p>Description: This event is fired when an offer is a redirect and [!DNL Target] will redirect to a different URL.|
|mbox|String|mbox name|
|message|String|Contains human-readable description, such as what happened, the error message, etc.|
|tracking|Object|Contains the `sessionId` and `deviceId`. In some cases, `deviceId` could be missing because [!DNL Target] couldn't retrieve it from edge server.|
|type|String|**On-device decisioning artifact succeeded**<p>Constant:<p>`adobe.target.event.ARTIFACT_DOWNLOAD_SUCCEEDED`<p>String value: `artifactDownloadSucceeded`<p>Description: Called when the on-device decisioning artifact is successfully downloaded.<p>**On-device decisioning artifact failed**<p>Constant: `adobe.target.event.ARTIFACT_DOWNLOAD_FAILED`<p>String Value: `artifactDownloadFailed`<p>Description: Called when the on-device decisioning artifact failed to download.| 

## Usage

```javascript {line-numbers="true"}
document.addEventListener(adobe.target.event.REQUEST_SUCCEEDED, function(event) { 
  console.log('Event', event); 
});
```

## Training Video: Response Tokens and the at.js Custom Events ![Tutorial badge](../../../assets/tutorial.png)

Watch the following video to learn how to use Response Tokens and at.js Custom Events to share profile information from [!DNL Target] to third-party systems.

>[!VIDEO](https://video.tv.adobe.com/v/23253/?quality=12)
