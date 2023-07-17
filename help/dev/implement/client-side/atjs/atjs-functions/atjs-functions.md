---
keywords: at.js, functions, javascript library
description: View a list of functions that can be used with the 1.x and 2.x versions of the at.js JavaScript library in [!DNL Adobe Target].
title: What Functions Can I Use with at.js?
feature: at.js
exl-id: 1efed365-8a74-4c85-bdb1-8daaaf53d642
---
# at.js functions

List of functions that can be used with the [!DNL Adobe Target] at.js JavaScript library. Click the links in the Function column for more information and examples.

|Function|Details|
| --- | --- | 
|[[!UICONTROL adobe.target.getOffer(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffer.md)|This function fires a request to get a [!DNL Target] offer. Use with `adobe.target.applyOffer()` to process the response or use your own success handling.|
|[[!UICONTROL adobe.target.getOffers(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-getoffers-atjs-2.md)<P>(at.js 2.x)|This function lets you retrieve multiple offers by passing in multiple mboxes. Additionally, multiple offers can be retrieved for all views in active activities.<P>**Note:** This function was introduced with at.js 2.x. This function is not available for at.js version 1.*x*.|
|[[!UICONTROL adobe.target.applyOffer(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffer.md)|This function is for applying the response content.|
|[[!UICONTROL adobe.target.applyOffers(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-applyoffers-atjs-2.md)<P>(at.js 2.x)|This function lets you apply more than one offer that was retrieved by [!UICONTROL adobe.target.getOffers()].<P>**Note:** This function was introduced with at.js 2.x. This function is not available for at.js version 1.*x*.|
|[[!UICONTROL adobe.target.triggerView (viewName, options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-triggerview-atjs-2.md)<P>(at.js 2.x)|This function can be called whenever a new page is loaded or when a component on a page is re-rendered.<P> This function should be implemented for single page applications (SPAs) in order to use the [!UICONTROL Visual Experience Composer] (VEC) to create [!UICONTROL A/B Test] and [!UICONTROL Experience Targeting] (XT) activities.|
|[[!UICONTROL adobe.target.trackEvent(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-trackevent.md)|This function fires a request to report user actions, such as clicks and conversions. It does not deliver activities in the response.|
|[[!UICONTROL mboxCreate(mbox,params)]](/help/dev/implement/client-side/atjs/atjs-functions/mboxcreate-atjs.md)<P>(at.js 1.x)|Executes a request and applies the offer to the closest DIV with mboxDefault class name.<P>**Note:** This function is available for at.js versions 1.*x* only. This function was deprecated with the release of at.js 2.x. This function returns default content if used with at.js 2.x.|
|[[!UICONTROL mboxDefine(options)] and [!UICONTROL mboxUpdate(options)]](/help/dev/implement/client-side/atjs/atjs-functions/mboxdefine-mboxupdate-atjs-1x.md)<P>(at.js 1.x)|Define and update an mbox.<P>**Note:** This function is available for at.js versions 1.*x* only. This function was deprecated with the release of at.js 2.x. This function returns default content if used with at.js 2.x.|
|[[!UICONTROL targetGlobalSettings(options)]](/help/dev/implement/client-side/atjs/atjs-functions/targetglobalsettings.md)|You can override settings in the at.js library using `[!UICONTROL targetGlobalSettings()]`, rather than configuring them in the [!DNL Target Standard/Premium] UI or by using REST APIs.<ul><li>Data Providers: This setting lets customers gather data from third-party data providers, such as Demandbase, BlueKai, and custom services, and pass the data to Target as mbox parameters in the global mbox request.</li></ul>|
|[[!UICONTROL targetPageParams(options)]](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparams.md)|This method allows you to attach parameters to the global mbox from outside of the request code.|
|[[!UICONTROL targetPageParamsAll(options)]](/help/dev/implement/client-side/atjs/atjs-functions/targetpageparamsall.md)|This method allows you to attach parameters to all mboxes from outside of the request code.|
|[[!UICONTROL registerExtension(options)]](/help/dev/implement/client-side/atjs/atjs-functions/registerextension-atjs-1x.md)<P>(at.js 1.x)|Provides a standard way to register a specific extension.<P>**Note:** This function is available for at.js versions 1.*x* only. This function was deprecated with the release of at.js 2.x. This function returns default content if used with at.js 2.x.|
|[[!UICONTROL at.js custom events]](/help/dev/implement/client-side/atjs/atjs-functions/atjs-custom-events.md)|at.js custom events let you know when an mbox request or offer fails or succeeds.|
|[[!UICONTROL adobe.target.sendNotifications(options)]](/help/dev/implement/client-side/atjs/atjs-functions/adobe-target-sendnotifications-atjs-21.md)<P>(at.js 2.1.0)|This function sends a notification to [!DNL Target] edge when an experience is rendered without using `[!UICONTROL adobe.target.applyOffer()]` or `[!UICONTROL adobe.target.applyOffers()]`.<P>**Note**: This function has been introduced in at.js 2.1.0 and will be available for any versions above 2.1.0.|
