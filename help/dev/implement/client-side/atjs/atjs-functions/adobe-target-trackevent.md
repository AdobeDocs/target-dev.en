---
keywords: adobe.target.trackEvent, trackEvent, trackevent, track event, at.js, functions, function, preventDefault, preventdefault, prevent default, adobe.target.trackEvent
description: Use the [!UICONTROL adobe.target.trackEvent()] function for the [!DNL Adobe Target] at.js JavaScript library to fire a request to report user actions, such as clicks and conversions on your site.
title: How Do I Use the [!UICONTROL adobe.target.trackEvent()] Function?
feature: at.js
exl-id: 9a55e4f1-d7f9-47c1-867c-2ce06fb26f9f
---
# [!UICONTROL adobe.target.trackEvent(options)]

This function fires a request to report user actions, such as clicks and conversions. It does not deliver activities in the response.

These event-tracking mbox calls can then be used to define metrics in activities. For more information, see [Success Metrics](https://experienceleague.adobe.com/docs/target/using/activities/success-metrics/success-metrics.html) and [Track Conversions](../how-to-deployatjs/implement-target-without-a-tag-manager.md#track-conversions).

Here are the API details:

| Key | Type | Required | Description |
|--- |--- |--- |--- |
|mbox|String|Yes|Mbox name<P>**Note**: If a [!UICONTROL trackEvent()] call is fired with an mbox name that has already fired on the page, the SDID of [!UICONTROL trackEvent()] is reset and will be different than the [!DNL Target] calls on the page. However, firing a [!UICONTROL trackEvent()] call with a different mbox name keeps the [!UICONTROL trackEvent()] call's SDID consistent with the [!UICONTROL Page Load Request]/[!UICONTROL triggerView()] calls on the page.|
|selector|String|No|CSS selectors used to find the HTML elements. The event listeners will be attached to found elements.|
|type|String|No|Represents a registered event type. It can be both HTML known events like: click, mousedown ,etc., as well as custom HTML events.|
|preventDefault|Boolean|No|Indicates whether to use `[!UICONTROL event.preventDefault()]` in the event listener callback. Defaults to false.<P>**Note**: Only `[!UICONTROL form[submit]]` and `a[click]` are supported. Other scenarios are not supported due to complexity and huge amount of scenarios to support.|
|params|Object|No|Mbox parameters. An object of key-value pairs that has the following structure:<P>`{ "param1": "value1", "param2": "value2"}`|
|timeout|Number|No|Timeout in milliseconds.<P>If not specified, default value is used:<P>`...timeoutInSeconds: 0.15...}`|
|success|Function|No|A callback function used to signal that event has been reported.|
|error|Function|No|A callback function used to signal that event could not be reported.|

## Example

```javascript {line-numbers="true"}
<a href="https://asite.com">click me!</a> 
```

plus javaScript code to assign `trackEvent`:

```javascript {line-numbers="true"}
<script> 
$('a').click(function(event){ 
  adobe.target.trackEvent({'mbox':'homePageHero'}) 
}); 
</script> 
```

Or:

```javascript {line-numbers="true"}
adobe.target.trackEvent({ 
    "mbox": "clicked-cta", 
    "params": { 
        "param1": "value1" 
    } 
});
```

>[!WARNING]
>
>If the mandatory fields are not set, no request is executed, and an error is thrown.
