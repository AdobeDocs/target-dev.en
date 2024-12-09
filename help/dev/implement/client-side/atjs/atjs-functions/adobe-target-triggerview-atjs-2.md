---
keywords: adobe.target.triggerView, triggerView, triggerview, trigger view, at.js, functions, function, viewName, viewname, view name, adobe.target.triggerView1
description: Use the adobe.target.triggerView() function for the [!DNL Adobe Target] at.js JavaScript library for use in Single Page Applications (SPAs). (at.js 2.x)
title: How Do I Use the adobe.target.triggerView() Function?
feature: at.js
exl-id: d6130c56-4e77-4668-ad21-a5b335f8b234
---
# adobe.target.triggerView (viewName, options) - at.js 2.x

This function can be called whenever a new page is loaded or when a component on a page is re-rendered. `adobe.target.triggerView()` should be implemented for single page applications (SPAs) to use the [!UICONTROL Visual Experience Composer] (VEC) to create [!UICONTROL A/B Test] and [!UICONTROL Experience Targeting] (XT) activities. If `[!UICONTROL adobe.target.triggerView()]` is not implemented on the site, the VEC cannot be used for SPAs. For more information, see [Single Page Application implementation](/help/dev/implement/client-side/atjs/how-to-deployatjs/target-atjs-single-page-application.md).

>[!NOTE]
>
>This function was introduced with at.js 2.*x*. This function is not available for at.js version 1.*x*.

|Parameter|Type|Required?|Description|
| --- | --- | --- | --- |
|viewName|String|Yes|Pass in any name as a string type that you want to represent your view. This view name appears in the [!UICONTROL Modifications] panel of the VEC for marketers to create actions and run their [!UICONTROL A/B Test] and [!UICONTROL Experience Targeting] XT activities.|
|options|Object|No||
|options > page|Boolean|No|**TRUE:** Default value of page is true. When page=true, notifications are sent to the [!DNL Target] backend for incrementing impression count.<P>A notification is always sent by default when a `[!UICONTROL triggerView]` is called, except when options > page is set to false.<P>**FALSE:** When page=false, notifications are not sent for incrementing impression count. This approach should be used when you want to only re-render a component on a page with an offer.<P>**Note**: Custom Code offers in the VEC are not re-rendered when `[!UICONTROL triggerView()]` is called with `{page: false}` as the option.|

## Example: True

`[!UICONTROL triggerView()]` call to send a notification to the [!DNL Target] backend for incrementing activity impressions and other metrics.

```javascript {line-numbers="true"}
adobe.target.triggerView("homeView")
```

## Example: False

`[!UICONTROL triggerView()]` call to not have notifications sent to the [!DNL Target] backend for impression counting.

```javascript {line-numbers="true"}
adobe.target.triggerView("homeView", {page: false})
```

## Example: Promise chaining with `getoffers()` and `applyOffers()`

To execute `triggerView()` when the `getOffers()` promise is resolved, it is important to execute `triggerView()` on the final block, as shown in the example below. This is necessary for the VEC to detect `Views` in authoring mode. 

```javascript {line-numbers="true"}
adobe.target.getOffers({
    'request': {
        'prefetch': {
            'views': [{
                'parameters': {}
            }]
        }
    }
}).then(function(response) {
    // Apply Offers
    adobe.target.applyOffers({
        response: response
    });
}).catch(function(error) {
    console.log("AT: getOffers failed - Error", error);
}).finally(() => {
    // Trigger View call, assuming pageView is defined elsewhere
    adobe.target.triggerView(pageView, {
        page: true
    });
    console.log('AT: View triggered on : ' + pageView);
});
```

## Example: Best compatibility for `triggerView()` with the [!UICONTROL Adobe Visual Editing Helper extension]

Consider the following when using the [Adobe Visual Editing Helper extension](https://experienceleague.adobe.com/en/docs/target/using/experiences/vec/troubleshoot-composer/visual-editing-helper-extension){target=_blank}:

Due to [!DNL Googl]e's new V3 Manifest policies for [!DNL Chrome] extensions, the [!UICONTROL Visual Editing Helper extension] must wait for the `DOMContentLoaded` event before loading the [!DNL Target] libraries in the VEC. This delay might cause web pages to fire the `triggerView()` call before the authoring libraries are ready, resulting in the view not being populated on load.

To mitigate this issue, use a listener for the page `load` event. 

Here's an example implementation:

```javascript
function triggerViewIfLoaded() {
    adobe.target.triggerView("homeView");
}

if (document.readyState === "complete") {
    // If the page is already loaded
    triggerViewIfLoaded();
} else {
    // If the page is not yet loaded, set up an event listener
    window.addEventListener("load", triggerViewIfLoaded);
}
```


